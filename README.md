# Quick start guide

## Download

Using `pip`:

    pip install -e git://github.com/ff0000/sortable.git#egg=sortable

Using `git`:

    git clone git://github.com/ff0000/sortable.git

or download the package from [github.com/ff0000/sortable](https://github.com/ff0000/sortable).

## Installation

Open `settings.py` and add `sortable` to your `INSTALLED_APPS`:

    INSTALLED_APPS = (
      [...],
      'sortable',
    )

Copy the reorder Javascript the `static/js` folder:

    cp [sortable folder]/sortable/static/js/admin_list_reorder.js [django-app]/static/js/

## Reordering instances of a model with drag-and-drop in the admin

To add the sortable feature a model called `Article` do the following:

Edit `app/articles/models.py` changing `models.Model` with `Sortable`:

    from sortable.models import Sortable

    class Article(Sortable):
      # here the model fields, Meta, etc.

Edit `app/articles/admin.py` changing `admin.ModelAdmin` with `SortableAdmin`:

    from sortable.admin import SortableAdmin
    
    class ArticleAdmin(SortableAdmin):
      # here the admin stuff 

If `ArticleAdmin` includes the `list_display` declaration, change it like this:

    # Old version
    list_display = ('__unicode__', ...,)
    # New version
    list_display = SortableAdmin.list_display + ('__unicode__', ...,)
    