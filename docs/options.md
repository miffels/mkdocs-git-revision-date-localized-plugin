# Options

You can customize the plugin by setting options in `mkdocs.yml`. For example:

```yaml
plugins:
  - git-revision-date-localized:
      type: timeago
      timezone: Europe/Amsterdam
      locale: en
      fallback_to_build_date: false
      enable_creation_date: true
      exclude:
          - index.md
```

## `type`

Default is `date`. The format of the date to be displayed. Valid values are `date`, `datetime`, `iso_date`, `iso_datetime` and `timeago`. Example outputs:

```
28 November, 2019           # type: date (default)
28 November, 2019 13:57:28  # type: datetime
2019-11-28                  # type: iso_date
2019-11-28 13:57:26         # type: iso_datetime
20 hours ago                # type: timeago
```

## `timezone`

Default is `UTC`. Specify a time zone database name ([reference](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)). This option is especially relevant when using `type: datetime` and `type: iso_datetime`. Note that when using [timeago](http://timeago.yarp.com/) (with `type: timeago`) any difference in time zones between server and client will be handled automatically.

## `locale`

Default is `None`. Specify a two letter [ISO639](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) language code to display dates in your preferred language.

- When not set, this plugin will look for `locale` or `language` options set in your theme. If also not set, the fallback is English (`en`)
- When used in combination with `type: date` or `type: datetime`, translation is done using [babel](https://github.com/python-babel/babel) which supports [these locales](http://www.unicode.org/cldr/charts/latest/supplemental/territory_language_information.html)
- When used in combination with `type: timeago` then [timeago.js](https://github.com/hustcc/timeago.js) is added to your website, which supports [these locales](https://github.com/hustcc/timeago.js/tree/master/src/lang). If you specify a locale not supported by timeago.js, the fallback is English (`en`)

Example outputs:

```
27 April, 2021                # `locale: en` with `type: date` (default)
27 April, 2021 13:11:28       # `locale: en` with `type: datetime`
2 weeks ago                   # `locale: en` with `type: timeago`
27 de marzo de 2021           # `locale: es` with `type: date`
27 de marzo de 2021 13:57:28  # `locale: es` with `type: datetime`
hace 2 semanas                # `locale: es` with `type: timeago`
```

## `fallback_to_build_date`

Default is `false`. Enables falling back to the time when `mkdocs build` was executed *when git is not available*. This means the revision date will be incorrect, but this can be acceptable if you want your project to also successfully build in environments with no access to GIT.

## `enable_creation_date`

Default is `false`. Enables adding a *Created* date at the bottom of each page on [supported themes](getting-started.md#supported-themes). Also enables use of <code>\{\{ git_creation_date_localized }}</code> in markdown files and `page.meta.git_creation_date_localized` in page templates.

## `exclude`

Default is empty. Specify a list of page source paths (one per line) that should not have a revision date included (excluded from processing by this plugin). This can be useful for example to remove the revision date from the front page. The source path of a page is relative to your `docs/` folder. You can also use [globs](https://docs.python.org/3/library/glob.html) instead of full source paths. To exclude `docs/subfolder/page.md` specify in your `mkdocs.yml` a line under `exclude:` with `- subfolder/page.md`. Some examples:

```yaml
# mkdocs.yml
plugins:
  - git-revision-date-localized:
      exclude:
        - index.md
        - subfolder/page.md
        - another_page.md
        - folder/*
```
