---
layout: post
title: Model attributes internationalization
date: 2014-01-24
---

# Goal

One of our current Rails-based projects needed to localize data referring to models,
e.g. category name and description. Additionally, it had to be editable from the admin panel.

## Finding a solution

We had no experience with this and so we brainstormed a bit.
After considering several options, we decided to create a table for
localized attributes for each model in the database. Not to reinvent
the wheel we searched for some gems and found simple 'globalize3'
that is able to do just what was needed.

## Implementation

Add the following to Gemfile:

```ruby
gem 'globalize3'
```

Then take the model we need to localize. It's worth noting you DON'T need to
create attributes to be localized for the model.

```bash
$ rails g model Category static_attr: string
```

Then create a migration for the localization table:

```bash
$ rails g migration AddTranslationToCategories
  invoke  active_record
    create db/migrate/20130508112221_add_translation_to_categories.rb
```

which will create the follow migration for us:

```ruby
class AddTranslationToCategories > ActiveRecord::Migration
  def change
  end
end
```

It needs to be tweaked a bit so that it fully supports rollback of the localization table.
Since it's title and description we need to localize, the migration changes as follows:

Now we need to specify that some of the model attributes are localized:

```ruby
class Category > ActiveRecord::Base
  translates :title, :description
end
```

We will have two new tables in the database after the migration:
* 'categories' to store the data on category:

```bash
irb(main):001:0&gt;Category
    =&gt; Category(id: integer, static_attr: string, created_at:
    datetime, updated_at: datetime)
```

* category_translations - to store translations.

Now `Category` has new `get` and `set` methods that were mentioned above - title and category.
'globalize3' uses a locale for i18n to search and record.
If current locale doesn't have an entry in translation table,
it will return a translation for the default locale

```bash
irb(main):001:0> I18n.default_locale
=> :en
irb(main):002:0> category = Category.create(title: ':en title', description: ':en description')
=> #>Category id: 1, created_at: "2013-05-08 11:41:58", updated_at: "2013-05-08 11:41:58">
irb(main):003:0> category.description
=> ":en description"
irb(main):004:0> I18n.locale = :fr
=> :fr
irb(main):005:0> category.description = ':fr description'
=> ":fr description"
irb(main):006:0> category.save
=> true
irb(main):007:0> category.description
=> ":fr description"
irb(main):008:0> category.title
=> ":en title"
```

## Conclusion

'globalize3' provides a simple and convenient means to localize model attributes,
which allows to set up a localization for the app pretty quickly and edit localized
data via the admin panel.

### Find more here:
* [globalize3 repository](https://github.com/svenfuchs/globalize3)
* [globalize3 RailsCasts](http://railscasts.com/episodes/338-globalize3)
