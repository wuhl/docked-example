# Instructions
Based on https://github.com/rails/docked and https://github.com/driftingruby/template

Example Drifting Ruby #326 Dabbling with Turbo: https://www.youtube.com/watch?v=aEvvDgC_D9Q

# Start Docker
Start "Docker Desktop"

# If not yet done
```
$ docker volume create ruby-bundle-cache
```

# Install alias
```
$ alias docked='docker run --rm -it -v ${PWD}:/rails -v ruby-bundle-cache:/bundle -p 3000:3000 ghcr.io/rails/cli'
```

# Create your rails app
```
$ docked rails new myrails --skip-jbuilder --javascript esbuild --css bootstrap
```

# Add template
```
$ cp -R driftingruby myrails
$ cd myrails
$ docked rails app:template LOCATION=driftingruby/template.rb
```

# Create projects model and database
```
$ docked rails generate scaffold project name active:boolean
$ docked rails db:migrate
```

# Add some data in file "seeds.rb"
```
...
Project.create(name: "My First Project", active: true)
Project.create(name: "My Second Project", active: true)
Project.create(name: "My Third Project", active: true)
Project.create(name: "My Fourth Project", active: true)
Project.create(name: "My Fifth Project", active: true)
```

# And seed the data
```
$ docked rails db:seed
```

# Add menue entry in file "_navigation_links.html.erb"
```
...
<li class="nav-item me-4">
  <%= link_to "Projects", projects_path, class: 'nav-link' %>
</li>
```

# Start server: Foreman, Yarn and Puma
```
$ docked bin/dev
```

# Add some bradcast stuff
## Add turbo stream on top in file "_project.html.erb"
```
<%= turbo_stream_from project %>
...
```

## And the broadcsts symbol in the model file "project.rb"
```
class Project < ApplicationRecord
  broadcasts
end
```

# Url
```
http://localhost:3000/projects
```
