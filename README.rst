Quick start guide
=================

Installation
------------
::

    pip install django-sortable-fc

Open ``settings.py`` and add ``sortable`` to your ``INSTALLED_APPS``::

    INSTALLED_APPS = (
      [...],
      'sortable',
    )

Reordering instances of a model with drag-and-drop in the admin
---------------------------------------------------------------

To add the sortable feature a model called ``Article`` do the following:

Edit ``app/articles/models.py`` changing ``models.Model`` with
``Sortable``::

    from sortable.models import Sortable

    class Article(Sortable):
      # here the model fields, Meta, etc.

If ``Meta`` is present, inherit from ``Sortable.Meta``::

    # Old version
    class Meta:
    # New version
    class Meta(Sortable.Meta):

Edit ``app/articles/admin.py`` changing ``admin.ModelAdmin`` with
``SortableAdmin``::

    from sortable.admin import SortableAdmin

    class ArticleAdmin(SortableAdmin):
      # here the admin stuff

If ``ArticleAdmin`` includes the ``list_display`` declaration, change it
like this::

    # Old version
    list_display = ('__unicode__', ...,)
    # New version
    list_display_links = ('__unicode__', )
    list_display = SortableAdmin.list_display + ('__unicode__', ...,)

The ``list_display_links`` indicates which field will show the admin
detail page when clicked.
