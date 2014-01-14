# Source code for static site

Minimalistic site on middleman that uses slim, sass and coffeescript

###Prepare development environment###

```bash
  git clone git@github.com:fs/static-base.git sitename
  cd sitename
  bin/bootstrap
```

## Development workflow

1. Start server with `bin/server`
2. Make changes in the `source` folder
3. Checkout results in the browser on `http://localhost:4567`

## Manual deploy to Github pages

Run `bin/deploy`

Make sure you have specified correct `source/CNAME`

## Semaphore integration

### Test build

You can use [Semaphore](https://semaphoreapp.com) to make sure you source code
will be build successfully.

Add these build commands:

```bash
bin/bootstrap
bin/build
```

### Deploy automatically to Github pages

* Deploy type: `Capistrano`
* Deployment Strategy: `Manual`
* Deploy commands:

```bash
# git identity required for git push
git config --global user.email "firstname.lastname+semaphore@flatstack.com"
git config --global user.name "Semaphore"
bin/deploy
```
* SSH key: specify your ssh key or unique per project.
