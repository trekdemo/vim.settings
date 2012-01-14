require 'fileutils'

desc "link ViM configuration files."
task :link_vim_conf_files do
  %w[ vimrc.after vimrc.before gvimrc.after gvimrc.before ].each do |file|
    dest = File.expand_path("~/.#{file}")
    unless File.exist?(dest)
      FileUtils.ln_sf(File.expand_path("../.vim.settings/#{file}", __FILE__), dest)
    end
  end
end

task :update do
  puts "Synchronising submodules urls"
  `git submodule sync > /dev/null`

  puts "Updating the submodules"
  `git submodule update --init > /dev/null`
end

task :install => [:link_vim_conf_files] do
  # Dummy task, real work is done with the hooks.
end

desc "Install or Update Janus."
task :default do
  sh "rake update"
  sh "rake install"
end
