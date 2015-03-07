desc 'Setup'
task :setup do
  mkdir_p 'original'
  Dir.chdir 'original' do
    unless Dir.exists?('BackstopJS')
      sh "git clone https://github.com/garris/BackstopJS.git"
    end
    Dir.chdir 'BackstopJS' do
      sh 'npm install'
    end
  end

  mkdir_p 'addCookie'
  Dir.chdir 'addCookie' do
    unless Dir.exists?('BackstopJS')
      sh "git clone https://github.com/kyanny/BackstopJS.git"
    end
    Dir.chdir 'BackstopJS' do
      sh "git checkout addCookie"
      sh 'npm install'
    end
  end
end

desc 'Run (original)'
task :original => :stop do
  Dir.chdir 'original/BackstopJS' do
    sh 'gulp reference'
    sh 'gulp test'
  end
end

desc 'Run (addCookie)'
task :addCookie => :stop do
  unless File.exists?('cookies.json')
    raise RuntimeError, 'cookies.json does not exist'
  end
  cp 'cookies.json', 'addCookie/BackstopJS/cookies.json'
  Dir.chdir 'addCookie/BackstopJS' do
    sh 'gulp reference'
    sh 'gulp test'
  end
end

desc 'Stop'
task :stop do
  Dir.chdir 'original/BackstopJS' do
    sh 'gulp stop'
  end
  Dir.chdir 'addCookie/BackstopJS' do
    sh 'gulp stop'
  end
end

desc 'Clean'
task :clean => :stop do
  rm_rf 'original'
  rm_rf 'addCookie'
end

task :default => :setup
