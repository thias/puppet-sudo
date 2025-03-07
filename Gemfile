source ENV['GEM_SOURCE'] || "https://rubygems.org"

def location_for(place, version = nil)
  if place =~ /^(git[:@][^#]*)#(.*)/
    [version, { :git => $1, :branch => $2, :require => false}].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false}]
  else
    [place, version, { :require => false}].compact
  end
end

group :development, :unit_tests do
  gem 'json',                      :require => false
  gem 'metadata-json-lint',        :require => false
  gem 'puppet_facts',              :require => false
  gem 'puppet-blacksmith',         :require => false
  gem 'puppetlabs_spec_helper',    :require => false
  gem 'rspec-puppet', '>= 2.3.2',  :require => false
  gem 'simplecov',                 :require => false
end
group :system_tests do
  gem 'beaker-rspec',                  *location_for(ENV['BEAKER_RSPEC_VERSION'] || '>= 3.4')
  gem 'beaker',                        *location_for(ENV['BEAKER_VERSION'])
  gem 'serverspec',                    :require => false
  gem 'beaker-puppet_install_helper',  :require => false
  gem 'master_manipulator',            :require => false
  gem 'beaker-hostgenerator',          *location_for(ENV['BEAKER_HOSTGENERATOR_VERSION'])
end

gem 'facter', *location_for(ENV['FACTER_GEM_VERSION'])
gem 'puppet', *location_for(ENV['PUPPET_GEM_VERSION'])


if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end
