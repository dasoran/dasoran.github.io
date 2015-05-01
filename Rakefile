REPOSITORY = 'https://$GH_TOKEN@github.com/dasoran/dasoran.github.io.git'

define_method(:build_jekyll_pages) { sh 'bundle exec jekyll build --destination ../blog' }

desc 'Clone blog repository to _deploy directory and checkout master branch'
task :setup do
  sh 'rm -rf  _deploy'
  sh "git clone #{REPOSITORY} _deploy"
  cd('_deploy') { sh 'git checkout master' }
end

desc 'deploy static pages to master automatically via Travis-CI'
task :autodeploy do
  cd '_deploy/blogsource' do
    build_jekyll_pages
  end
  cd '_deploy' do
    sh 'git add -A'
    sh 'git commit -m "Update via Travis"'
    sh "git push --quiet #{REPOSITORY} master 2> /dev/null"
  end
end

