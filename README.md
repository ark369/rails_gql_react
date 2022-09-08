# Learning rails + graphql + react

## Setup
Following https://gorails.com/setup/windows/10

### Installing Ruby
```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev
```

```
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

```
rbenv install 3.1.2
rbenv global 3.1.2
```

```
gem install bundler
rbenv rehash
```

### Installing Rails
```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list

sudo apt update
sudo apt-get install -y nodejs yarn
```

```
gem install rails -v 7.0.2.4
rbenv rehash
```

## Bootstrapping

Following the guide at ~https://egghead.io/blog/rails-graphql-typescript-react-apollo~ https://towardsdev.com/set-up-rails-7-with-graphql-apollo-client-and-react-72f63a9a3b54 (looks like the first guide was pre-Rails v7, which no longer includes webpack).

Still used the first guide to set up the rails application and model.

```
rails new books
cd books
rails g model book title:string
rails db:migrate
```

Add a book inside `rails c` (console)
```
Book.create!(title: "Active Rails")
```

Adding graphql:
```
bundle add graphql
rails generate graphql:install
bundle install
```

Generate gql type:
```
rails generate graphql:object book
```

Start Rails server:
```
rails server
```

In browser, navigate to http://localhost:3000/graphiql, then run the query:
```
query allBooks {
  books {
    id
    title
  }
}
```