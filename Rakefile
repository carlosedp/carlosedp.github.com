desc 'build'
task :build do
    puts 'Compiling Compass CSS'
    sh "compass compile"
    end
end

desc 'deploy'
task :deploy => [:build] do
    # uploads ALL files b/c I often do site-wide changes and prefer overwriting all
    puts 'DEPLOYING TO Server'
    git push origin master
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

