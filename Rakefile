require 'pry'
require 'fileutils'

namespace :greetings do
  desc "prints thank you"
  task :thank_you do
    puts "thank you"
  end

  desc "prints hello name"
  task :hello_name, [:name] do |cmd, args|
    puts "hello, #{args[:name]}"
  end
end

desc "print default message"
task :default do
  puts "hello i'm the default task"
end

namespace :cake do

  desc "Bake a Cake"
  task :bake => [:mix_up, :go_to_store] do
    puts "Cake is baked"
  end

  task :mix_up => [:add_flower, :add_eggs] do
    puts "Mix up ingredients"
  end

  task :add_flower => :get_flower do
    puts "Adding flower"
  end

  task :add_eggs => :go_to_store do
    puts "Adding Eggs"
  end

  task :get_flower => :go_to_store do
    puts "Get Flower"
  end

  task :go_to_store do
    puts "Go to Store"
  end

  desc "can't spell"
  task :learn_how_to_spell, [:word] do |cmd, args|
    puts "need to learn how to spell, #{args[:word]}"
  end
end

namespace :dozer do
  desc "print ENV"
  task :env do
    sh("ENV")
  end

  desc "print pwd"
  task :pwd do
    sh("pwd")
  end

  # desc "adds views for a resource"
  # task :make_views do
  #   sh("mkdir views_test")
  #   sh("touch views_test/index.erb")
  #   sh("touch views_test/show.erb")
  #   sh("touch views_test/edit.erb")
  #   sh("touch views_test/new.erb")
  # end

  desc "adds views for a resource name"
  task :make_views, [:resource] do |cmd, args|
    sh("mkdir views/#{args[:resource]}")
    sh("touch views/#{args[:resource]}/index.erb")
    sh("touch views/#{args[:resource]}/new.erb")
    sh("touch views/#{args[:resource]}/show.erb")
    sh("touch views/#{args[:resource]}/edit.erb")
  end

end

namespace :db do
  desc "create a DB called dvr_app_test"
  task :create, [:dbname] do |cmd, args|
    dbname = args[:dbname] || "dvr_app_test"
    sh("createdb #{args[:dbname]}")
    sh("touch #{args[:dbname]}/schema.sql")
    sh("touch #{args[:dbname]}/seeds.rb")
  end

  desc "drop db"
  task :drop do
    sh("drop dvr_app_test")
  end

  desc "seed my db"
  task: seed, [:env] do |cmd, args|
    # default environment
    env = args[:env] || "development"
    # load up my sinatra environment
    # populate my db
    # calls rake environment[env]
    Rake::Task['environment'].invoke(env)
    require './db/seeds'
  end

end

namespace :bundler do
  task :setup do
    require 'rubygems'
    require 'bundler'
  end
end

task :environment, [:env] => 'bundler:setup' do |cmd, args|
  ENV["RACK_ENV"] = args[:env] || "development"
  Bundler.require(:default, ENV["RACK_ENV"])
  require "./config/boot"
end

