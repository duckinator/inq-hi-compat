require "bundler/gem_tasks"
require "json"
require "net/http"
require "uri"

task :prepare_file do
  uri  = URI("https://rubygems.org/api/v1/gems/inq.json")
  data = Net::HTTP.get(uri)
  hash = JSON.parse(data)
  version = hash["version"]

  File.write("INQ_VERSION", version)
end

task :commit_and_push do
  version = File.read("INQ_VERSION")
  sh "git commit -am 'Version bump to #{version}'"
  sh "git push"
end

task :prepare => [:prepare_file, :commit_and_push]
