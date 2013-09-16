---
layout: post
title: "修改jekyllbootstrap的rakefile文件，让其可以指定创建的目录"
category: 
tags: [jekyllbootstrap,rakefile]
---
jekyllbootstrap中使用rake很不错，但是jekyll bootstrap提供的rake post命令却无法指定目录，实在是
太不方便（也许有吧），所以修改了一下jekyllbootstrap的Rakefile:

    # Usage: rake post title="A Title"
    desc "Begin a new post in #{CONFIG['posts']}"
    task :post do
      abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
      title = ENV["title"] || "new-post"
    #path创建的目录 Usage:rake post tile="A Title" path="directory/directory2" 
      path = ENV["path"] || ""
    #去掉目录中的特殊字符，除了/之外，去掉所有的特殊字符
      path = File.join(CONFIG['posts'],path.gsub(/[^\w\/]/,''))
    #除了-之外去掉所有的字符
      slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
    #把path目录添加进去
      filename = File.join(path,"#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['post_ext']}")
      if File.exist?(filename)
        abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
      end
      FileUtils.mkdir_p(path) unless Dir.exists?(path)
      puts "Creating new post: #{filename}"
      open(filename, 'w') do |post|
        post.puts "---"
        post.puts "layout: post"
        post.puts "title: \"#{title.gsub(/-/,' ')}\""
        post.puts "category: "
        post.puts "tags: []"
        post.puts "---"
        post.puts "{% include JB/setup %}"
      end
    end # task :post

