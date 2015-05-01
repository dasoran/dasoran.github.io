REPOSITORY = 'https://$GH_TOKEN@github.com/dasoran/dasoran.github.io.git'

define_method(:build_jekyll_pages) { sh 'bundle exec jekyll build --destination ../../blog' }
define_method :replace_blog_in_master_branch do 
  sh 'git checkout master'
  sh 'rm -rf ../blog'
  sh 'mv ../../blog ../'
end

desc 'Clone blog repository to _deploy directory and checkout master branch'
task :setup do
  sh 'rm -rf  _deploy'
  sh "git clone #{REPOSITORY} _deploy"
  cd('_deploy') { sh 'git checkout source' }
end

desc 'deploy static pages to master automatically via Travis-CI'
task :autodeploy do
  cd '_deploy/blogsource' do
    build_jekyll_pages
    replace_blog_in_master_branch
  end
  cd '_deploy' do
    sh 'git add -A blog'
    sh 'git commit -m "[ci skip] Update via Travis"'
    sh "git push --quiet #{REPOSITORY} master 2> /dev/null"
  end
end

