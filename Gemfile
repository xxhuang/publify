source 'https://rubygems.org'

if ENV["HEROKU"]
  ruby '2.1.5'

  gem "pg"
  gem "thin" # Change this to another web server if you want (ie. unicorn, passenger, puma...)
  gem "rails_12factor"
else

  require 'yaml'
  env = ENV["RAILS_ENV"] || 'development'
  dbfile = File.expand_path("../config/database.yml", __FILE__)

  unless File.exists?(dbfile)
    if ENV['DB']
      FileUtils.cp "config/database.yml.#{ENV['DB'] || 'postgres'}", 'config/database.yml'
    else
      raise "You need to configure config/database.yml first"
    end
  end

  conf = YAML.load(File.read(dbfile))
  environment = conf[env]
  adapter = environment['adapter'] if environment
  raise "You need define an adapter in your database.yml or set your RAILS_ENV variable" if adapter == '' || adapter.nil?
  case adapter
  when 'sqlite3'
    gem 'sqlite3'
  when 'postgresql'
    gem 'pg'
  when 'mysql2'
    gem 'mysql2'
  else
    raise "Don't know what gem to use for adapter #{adapter}"
  end
end

gem 'rails', '~> 4.1.8'
gem 'htmlentities'
gem 'bluecloth', '~> 2.1'
gem 'coderay', '~> 1.1.0'
gem 'kaminari'
gem 'RedCloth', '~> 4.2.8'
gem 'addressable', '~> 2.1', :require => 'addressable/uri'
gem 'mini_magick', '~> 3.8.1', :require => 'mini_magick'
gem 'uuidtools', '~> 2.1.1'
gem 'flickraw-cached'
gem 'rubypants', '~> 0.2.0'
gem 'rake', '~> 10.4.2'
#gem 'acts_as_list'
#gem 'acts_as_tree_rails3'
gem 'fog'
gem 'recaptcha', :require => 'recaptcha/rails', :branch => 'rails3'
gem 'carrierwave', '~> 0.10.0'
gem 'akismet', '~> 1.0'
gem 'twitter', '~> 5.12.0'

gem "jquery-rails", "~> 3.1.2"
gem "jquery-ui-rails", "~> 5.0.2"

gem 'rails-timeago', '~> 2.0'

gem 'rails_autolink', '~> 1.1.0'
gem 'dynamic_form', '~> 1.1.4'

gem 'non-stupid-digest-assets'

# removed from Rails-core as Rails 4.0
gem 'actionpack-page_caching', '~> 1.0.2'
gem 'rails-observers', '~> 0.1.2'

group :assets do
  gem 'sass-rails', " ~> 4.0.3"
  gem 'coffee-rails', " ~> 4.0.1"
  gem 'uglifier'
end

group :development, :test do
  gem 'thin'
  gem 'factory_girl', '~> 4.5.0'
  gem 'capybara'
  gem 'rspec-rails', '~> 3.1.0'
  gem 'simplecov', :require => false
  gem 'pry-rails'
  gem 'better_errors', '~> 2.0.0'
  gem 'binding_of_caller'
  gem 'guard-rspec'
  gem 'quiet_assets'
end

group :test do
  gem 'feedjira'
  gem "codeclimate-test-reporter", require: nil
end

# Install gems from each theme
Dir.glob(File.join(File.dirname(__FILE__), 'themes', '**', "Gemfile")) do |gemfile|
  eval(IO.read(gemfile), binding)
end
