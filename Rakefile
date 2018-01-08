require 'puppet-lint/tasks/puppet-lint'
require 'metadata-json-lint/rake_task'
PuppetLint.configuration.send('disable_80chars')
PuppetLint.configuration.send('disable_140chars')
PuppetLint.configuration.relative = true
PuppetLint.configuration.ignore_paths = ['spec/**/*.pp', 'pkg/**/*.pp', 'vendor/**/*.pp']

desc 'Validate manifests, templates, and ruby files'
task :validate do
  Dir['spec/**/*.rb', 'lib/**/*.rb'].each do |ruby_file|
    sh "ruby -c #{ruby_file}" unless ruby_file =~ /spec\/fixtures/
  end
  Dir['types/**/*.pp'].each do |manifest|
    sh "puppet parser validate #{manifest}"
  end
end
