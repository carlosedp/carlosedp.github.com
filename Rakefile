desc 'clean'
task :clean do
    puts 'Cleaning old ./_site dir'
    sh "rm -rf _site"
end

desc 'build'
task :build => [:clean] do
    puts 'Compiling Compass CSS'
    sh "compass compile"
    puts 'Building Jekyll site'
    sh "jekyll"
    sh %{growlnotify -t Jekyll -m 'carlosedp.com built'} do |ok, res|
        if ! ok
            puts 'Growlnotify not found.'
        end
    end
end

desc 'deploy via rsync'
task :deploy => [:clean, :build] do
    # uploads ALL files b/c I often do site-wide changes and prefer overwriting all
    puts 'DEPLOYING TO Server'
    # remove --rsh piece if not using 22
    sh "rsync -rtzh --progress --delete _site/ --rsh='ssh -p22' root@clyde.carlosedp.com:/var/www/carlosedp.com"
    puts 'done!'
    sh %{growlnotify -t Jekyll -m 'carlosedp.com deployed'} do |ok, res|
        if ! ok
            puts 'Growlnotify not found.'
        end
    end
end

desc 'run local server'
task :server => [:build] do
    puts 'Running local server'
    sh 'open http://localhost:4000'
    sh 'jekyll --server --auto'
end

desc 'Create new post markdown file'
task :post, [:post_title] do |t,args|
    require 'date'
    system "echo \"---\nlayout: post\ntitle: #{args.post_title}\ncomments: true\n---\" >  _posts/#{Date.today.year}-#{Date.today.strftime("%m")}-#{Date.today.strftime("%d")}-#{args.post_title.downcase.split(' ').join('-')}.md"
end

