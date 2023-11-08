- release notes
	- Django **3.1.9** fixes a security issue in 3.1.8.
		- ## CVE-2021-31542: Potential directory-traversal via uploaded files [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.9/#cve-2021-31542-potential-directory-traversal-via-uploaded-files)
		- MultiPartParser, UploadedFile, and FieldFile allowed directory-traversal via uploaded files with suitably crafted file names.
		- In order to mitigate this risk, stricter basename and path sanitation is now applied.
	- Django **3.1.10** fixes a security issue in 3.1.9.
		- ## CVE-2021-32052: Header injection possibility since   URLValidator   accepted newlines in input on Python 3.9.5+ [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.10/#cve-2021-32052-header-injection-possibility-since-urlvalidator-accepted-newlines-in-input-on-python-3-9-5)
		- On Python 3.9.5+, [URLValidator](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.URLValidator) didn’t prohibit newlines and tabs. If you used values with newlines in HTTP response, you could suffer from header injection attacks. Django itself wasn’t vulnerable because [HttpResponse](https://docs.djangoproject.com/en/4.2/ref/request-response/#django.http.HttpResponse) prohibits newlines in HTTP headers.
		- Moreover, the URLField form field which uses URLValidator silently removes newlines and tabs on Python 3.9.5+, so the possibility of newlines entering your data only existed if you are using this validator outside of the form fields.
		- This issue was introduced by the [bpo-43882](https://bugs.python.org/issue?@action=redirect&bpo=43882) fix.
	- Django **3.1.11** fixes a regression in 3.1.9.
		- ## Bugfixes [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.11/#bugfixes)
			- Fixed a regression in Django 3.1.9 where saving FileField would raise a SuspiciousFileOperation even when a custom [upload_to](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.FileField.upload_to) returns a valid file path ([#32718](https://code.djangoproject.com/ticket/32718)).
	- Django **3.1.12** fixes two security issues in 3.1.11.
		- ## CVE-2021-33203: Potential directory traversal via   admindocs [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.12/#cve-2021-33203-potential-directory-traversal-via-admindocs)
		- Staff members could use the [admindocs](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/admindocs/#module-django.contrib.admindocs) TemplateDetailView view to check the existence of arbitrary files. Additionally, if (and only if) the default admindocs templates have been customized by the developers to also expose the file contents, then not only the existence but also the file contents would have been exposed.
		- As a mitigation, path sanitation is now applied and only files within the template root directories can be loaded.
		- ## CVE-2021-33571: Possible indeterminate SSRF, RFI, and LFI attacks since validators accepted leading zeros in IPv4 addresses [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.12/#cve-2021-33571-possible-indeterminate-ssrf-rfi-and-lfi-attacks-since-validators-accepted-leading-zeros-in-ipv4-addresses)
		- [URLValidator](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.URLValidator), [validate_ipv4_address()](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.validate_ipv4_address), and [validate_ipv46_address()](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.validate_ipv46_address) didn’t prohibit leading zeros in octal literals. If you used such values you could suffer from indeterminate SSRF, RFI, and LFI attacks.
		- [validate_ipv4_address()](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.validate_ipv4_address) and [validate_ipv46_address()](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.validate_ipv46_address) validators were not affected on Python 3.9.5+.
	- Django **3.1.13** fixes a security issue with severity “high” in 3.1.12.
		- ## CVE-2021-35042: Potential SQL injection via unsanitized   QuerySet.order_by()   input [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.13/#cve-2021-35042-potential-sql-injection-via-unsanitized-queryset-order-by-input)
		- Unsanitized user input passed to QuerySet.order_by() could bypass intended column reference validation in path marked for deprecation resulting in a potential SQL injection even if a deprecation warning is emitted.
		- As a mitigation the strict column reference validation was restored for the duration of the deprecation period. This regression appeared in 3.1 as a side effect of fixing [#31426](https://code.djangoproject.com/ticket/31426).
		- The issue is not present in the main branch as the deprecated path has been removed.
	- Django **3.1.14** fixes a security issue with severity “low” in 3.1.13.
		- ## CVE-2021-44420: Potential bypass of an upstream access control based on URL paths [¶](https://docs.djangoproject.com/en/4.2/releases/3.1.14/#cve-2021-44420-potential-bypass-of-an-upstream-access-control-based-on-url-paths)
		- HTTP requests for URLs with trailing newlines could bypass an upstream access control based on URL paths.
	- ## Django 3.2 release notes [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-3-2-release-notes)
		- Welcome to Django 3.2!
		- These release notes cover the [new features](https://docs.djangoproject.com/en/4.2/releases/3.2/#whats-new-3-2), as well as some [backwards incompatible changes](https://docs.djangoproject.com/en/4.2/releases/3.2/#backwards-incompatible-3-2) you’ll want to be aware of when upgrading from Django 3.1 or earlier. We’ve [begun the deprecation process for some features](https://docs.djangoproject.com/en/4.2/releases/3.2/#deprecated-features-3-2).
		- See the [How to upgrade Django to a newer version](https://docs.djangoproject.com/en/4.2/howto/upgrade-version/) guide if you’re updating an existing project.
		- Django 3.2 is designated as a [long-term support release](https://docs.djangoproject.com/en/4.2/internals/release-process/#term-Long-term-support-release). It will receive security updates for at least three years after its release. Support for the previous LTS, Django 2.2, will end in April 2022.
		- ## Python compatibility [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#python-compatibility)
		- Django 3.2 supports Python 3.6, 3.7, 3.8, 3.9, and 3.10 (as of 3.2.9). We **highly recommend** and only officially support the latest release of each series.
		- ## What’s new in Django 3.2 [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#what-s-new-in-django-3-2)
		- ### Automatic   [AppConfig](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig)   discovery [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#automatic-appconfig-discovery)
		- Most pluggable applications define an [AppConfig](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig) subclass in an apps.py submodule. Many define a default_app_config variable pointing to this class in their __init__.py.
		- When the apps.py submodule exists and defines a single [AppConfig](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig) subclass, Django now uses that configuration automatically, so you can remove default_app_config.
		- default_app_config made it possible to declare only the application’s path in [INSTALLED_APPS](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-INSTALLED_APPS) (e.g. 'django.contrib.admin') rather than the app config’s path (e.g. 'django.contrib.admin.apps.AdminConfig'). It was introduced for backwards-compatibility with the former style, with the intent to switch the ecosystem to the latter, but the switch didn’t happen.
		- With automatic AppConfig discovery, default_app_config is no longer needed. As a consequence, it’s deprecated.
		- See [Configuring applications](https://docs.djangoproject.com/en/4.2/ref/applications/#configuring-applications-ref) for full details.
		- ### Customizing type of auto-created primary keys [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#customizing-type-of-auto-created-primary-keys)
		- When defining a model, if no field in a model is defined with [primary_key=True](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.Field.primary_key) an implicit primary key is added. The type of this implicit primary key can now be controlled via the [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) setting and [AppConfig.default_auto_field](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig.default_auto_field) attribute. No more needing to override primary keys in all models.
		- Maintaining the historical behavior, the default value for [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) is [AutoField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.AutoField). Starting with 3.2 new projects are generated with [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) set to [BigAutoField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.BigAutoField). Also, new apps are generated with [AppConfig.default_auto_field](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig.default_auto_field) set to [BigAutoField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.BigAutoField). In a future Django release the default value of [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) will be changed to [BigAutoField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.BigAutoField).
		- To avoid unwanted migrations in the future, either explicitly set [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) to [AutoField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.AutoField):
		- ```python
		  DEFAULT_AUTO_FIELD = "django.db.models.AutoField"
		  ```
		- or configure it on a per-app basis:
		- ```python
		  from django.apps import AppConfig
		  
		  class MyAppConfig(AppConfig):
		      default_auto_field = "django.db.models.AutoField"
		      name = "my_app"
		  ```
		- or on a per-model basis:
		- ```python
		  from django.db import models
		  
		  class MyModel(models.Model):
		      id = models.AutoField(primary_key=True)
		  ```
		- In anticipation of the changing default, a system check will provide a warning if you do not have an explicit setting for [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD).
		- When changing the value of [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD), migrations for the primary key of existing auto-created through tables cannot be generated currently. See the [DEFAULT_AUTO_FIELD](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-DEFAULT_AUTO_FIELD) docs for details on migrating such tables.
		- ### Functional indexes [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#functional-indexes)
		- The new [*expressions](https://docs.djangoproject.com/en/4.2/ref/models/indexes/#django.db.models.Index.expressions) positional argument of [Index()](https://docs.djangoproject.com/en/4.2/ref/models/indexes/#django.db.models.Index) enables creating functional indexes on expressions and database functions. For example:
		- ```python
		  from django.db import models
		  from django.db.models import F, Index, Value
		  from django.db.models.functions import Lower, Upper
		  
		  class MyModel(models.Model):
		      first_name = models.CharField(max_length=255)
		      last_name = models.CharField(max_length=255)
		      height = models.IntegerField()
		      weight = models.IntegerField()
		  
		  class Meta:
		      indexes = [
		          Index(
		              Lower("first_name"),
		              Upper("last_name").desc(),
		              name="first_last_name_idx",
		          ),
		          Index(
		              F("height") / (F("weight") + Value(5)),
		              name="calc_idx",
		          ),
		      ]
		  ```
		- Functional indexes are added to models using the [Meta.indexes](https://docs.djangoproject.com/en/4.2/ref/models/options/#django.db.models.Options.indexes) option.
		- ### pymemcache   support [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#pymemcache-support)
		- The new django.core.cache.backends.memcached.PyMemcacheCache cache backend allows using the [pymemcache](https://pypi.org/project/pymemcache/) library for memcached. pymemcache 3.4.0 or higher is required. For more details, see the [documentation on caching in Django](https://docs.djangoproject.com/en/4.2/topics/cache/).
		- ### New decorators for the admin site [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#new-decorators-for-the-admin-site)
		- The new [display()](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.display) decorator allows for easily adding options to custom display functions that can be used with [list_display](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.list_display) or [readonly_fields](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.readonly_fields).
		- Likewise, the new [action()](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/actions/#django.contrib.admin.action) decorator allows for easily adding options to action functions that can be used with [actions](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.actions).
		- Using the @display decorator has the advantage that it is now possible to use the @property decorator when needing to specify attributes on the custom method. Prior to this it was necessary to use the property() function instead after assigning the required attributes to the method.
		- Using decorators has the advantage that these options are more discoverable as they can be suggested by completion utilities in code editors. They are merely a convenience and still set the same attributes on the functions under the hood.
		- ### Minor features [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#minor-features)
		- #### [django.contrib.admin](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#module-django.contrib.admin) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-admin)
			- [ModelAdmin.search_fields](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.search_fields) now allows searching against quoted phrases with spaces.
			- Read-only related fields are now rendered as navigable links if target models are registered in the admin.
			- The admin now supports theming, and includes a dark theme that is enabled according to browser settings. See [Theming support](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#admin-theming) for more details.
			- [ModelAdmin.autocomplete_fields](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.autocomplete_fields) now respects [ForeignKey.to_field](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.ForeignKey.to_field) and [ForeignKey.limit_choices_to](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.ForeignKey.limit_choices_to) when searching a related model.
			- The admin now installs a final catch-all view that redirects unauthenticated users to the login page, regardless of whether the URL is otherwise valid. This protects against a potential model enumeration privacy issue.
		- Although not recommended, you may set the new [AdminSite.final_catch_all_view](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.AdminSite.final_catch_all_view) to False to disable the catch-all view.
		- #### [django.contrib.auth](https://docs.djangoproject.com/en/4.2/topics/auth/#module-django.contrib.auth) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-auth)
			- The default iteration count for the PBKDF2 password hasher is increased from 216,000 to 260,000.
			- The default variant for the Argon2 password hasher is changed to Argon2id. memory_cost and parallelism are increased to 102,400 and 8 respectively to match the argon2-cffi defaults.
			- Increasing the memory_cost pushes the required memory from 512 KB to 100 MB. This is still rather conservative but can lead to problems in memory constrained environments. If this is the case, the existing hasher can be subclassed to override the defaults.
			- The default salt entropy for the Argon2, MD5, PBKDF2, SHA-1 password hashers is increased from 71 to 128 bits.
		- #### [django.contrib.contenttypes](https://docs.djangoproject.com/en/4.2/ref/contrib/contenttypes/#module-django.contrib.contenttypes) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-contenttypes)
			- The new absolute_max argument for [generic_inlineformset_factory()](https://docs.djangoproject.com/en/4.2/ref/contrib/contenttypes/#django.contrib.contenttypes.forms.generic_inlineformset_factory) allows customizing the maximum number of forms that can be instantiated when supplying POST data. See [Limiting the maximum number of instantiated forms](https://docs.djangoproject.com/en/4.2/topics/forms/formsets/#formsets-absolute-max) for more details.
			- The new can_delete_extra argument for [generic_inlineformset_factory()](https://docs.djangoproject.com/en/4.2/ref/contrib/contenttypes/#django.contrib.contenttypes.forms.generic_inlineformset_factory) allows removal of the option to delete extra forms. See [can_delete_extra](https://docs.djangoproject.com/en/4.2/topics/forms/formsets/#django.forms.formsets.BaseFormSet.can_delete_extra) for more information.
		- #### [django.contrib.gis](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/#module-django.contrib.gis) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-gis)
			- The [GDALRaster.transform()](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/gdal/#django.contrib.gis.gdal.GDALRaster.transform) method now supports [SpatialReference](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/gdal/#django.contrib.gis.gdal.SpatialReference).
			- The [DataSource](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/gdal/#django.contrib.gis.gdal.DataSource) class now supports [pathlib.Path](https://docs.python.org/3/library/pathlib.html#pathlib.Path).
			- The [LayerMapping](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/layermapping/#django.contrib.gis.utils.LayerMapping) class now supports [pathlib.Path](https://docs.python.org/3/library/pathlib.html#pathlib.Path).
		- #### [django.contrib.postgres](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/#module-django.contrib.postgres) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-postgres)
			- The new [ExclusionConstraint.include](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/constraints/#django.contrib.postgres.constraints.ExclusionConstraint.include) attribute allows creating covering exclusion constraints on PostgreSQL 12+.
			- The new [ExclusionConstraint.opclasses](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/constraints/#django.contrib.postgres.constraints.ExclusionConstraint.opclasses) attribute allows setting PostgreSQL operator classes.
			- The new [JSONBAgg.ordering](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/aggregates/#django.contrib.postgres.aggregates.JSONBAgg.ordering) attribute determines the ordering of the aggregated elements.
			- The new [JSONBAgg.distinct](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/aggregates/#django.contrib.postgres.aggregates.JSONBAgg.distinct) attribute determines if aggregated values will be distinct.
			- The [CreateExtension](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/operations/#django.contrib.postgres.operations.CreateExtension) operation now checks that the extension already exists in the database and skips the migration if so.
			- The new [CreateCollation](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/operations/#django.contrib.postgres.operations.CreateCollation) and [RemoveCollation](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/operations/#django.contrib.postgres.operations.RemoveCollation) operations allow creating and dropping collations on PostgreSQL. See [Managing collations using migrations](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/operations/#manage-postgresql-collations) for more details.
			- Lookups for [ArrayField](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/fields/#django.contrib.postgres.fields.ArrayField) now allow (non-nested) arrays containing expressions as right-hand sides.
			- The new [OpClass()](https://docs.djangoproject.com/en/4.2/ref/contrib/postgres/indexes/#django.contrib.postgres.indexes.OpClass) expression allows creating functional indexes on expressions with a custom operator class. See [Functional indexes](https://docs.djangoproject.com/en/4.2/releases/3.2/#new-functional-indexes) for more details.
		- #### [django.contrib.sitemaps](https://docs.djangoproject.com/en/4.2/ref/contrib/sitemaps/#module-django.contrib.sitemaps) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-sitemaps)
			- The new [Sitemap](https://docs.djangoproject.com/en/4.2/ref/contrib/sitemaps/#django.contrib.sitemaps.Sitemap) attributes [alternates](https://docs.djangoproject.com/en/4.2/ref/contrib/sitemaps/#django.contrib.sitemaps.Sitemap.alternates), [languages](https://docs.djangoproject.com/en/4.2/ref/contrib/sitemaps/#django.contrib.sitemaps.Sitemap.languages) and [x_default](https://docs.djangoproject.com/en/4.2/ref/contrib/sitemaps/#django.contrib.sitemaps.Sitemap.x_default) allow generating sitemap *alternates* to localized versions of your pages.
		- #### [django.contrib.syndication](https://docs.djangoproject.com/en/4.2/ref/contrib/syndication/#module-django.contrib.syndication) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#django-contrib-syndication)
			- The new item_comments hook allows specifying a comments URL per feed item.
		- #### Database backends [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#database-backends)
			- Third-party database backends can now skip or mark as expected failures tests in Django’s test suite using the new DatabaseFeatures.django_test_skips and django_test_expected_failures attributes.
		- #### Decorators [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#decorators)
			- The new [no_append_slash()](https://docs.djangoproject.com/en/4.2/topics/http/decorators/#django.views.decorators.common.no_append_slash) decorator allows individual views to be excluded from [APPEND_SLASH](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-APPEND_SLASH) URL normalization.
		- #### Error Reporting [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#error-reporting)
			- Custom [ExceptionReporter](https://docs.djangoproject.com/en/4.2/howto/error-reporting/#django.views.debug.ExceptionReporter) subclasses can now define the [html_template_path](https://docs.djangoproject.com/en/4.2/howto/error-reporting/#django.views.debug.ExceptionReporter.html_template_path) and [text_template_path](https://docs.djangoproject.com/en/4.2/howto/error-reporting/#django.views.debug.ExceptionReporter.text_template_path) properties to override the templates used to render exception reports.
		- #### File Uploads [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#file-uploads)
			- The new [FileUploadHandler.upload_interrupted()](https://docs.djangoproject.com/en/4.2/ref/files/uploads/#django.core.files.uploadhandler.FileUploadHandler.upload_interrupted) callback allows handling interrupted uploads.
		- #### Forms [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#forms)
			- The new absolute_max argument for [formset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/formsets/#django.forms.formsets.formset_factory), [inlineformset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/models/#django.forms.models.inlineformset_factory), and [modelformset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/models/#django.forms.models.modelformset_factory) allows customizing the maximum number of forms that can be instantiated when supplying POST data. See [Limiting the maximum number of instantiated forms](https://docs.djangoproject.com/en/4.2/topics/forms/formsets/#formsets-absolute-max) for more details.
			- The new can_delete_extra argument for [formset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/formsets/#django.forms.formsets.formset_factory), [inlineformset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/models/#django.forms.models.inlineformset_factory), and [modelformset_factory()](https://docs.djangoproject.com/en/4.2/ref/forms/models/#django.forms.models.modelformset_factory) allows removal of the option to delete extra forms. See [can_delete_extra](https://docs.djangoproject.com/en/4.2/topics/forms/formsets/#django.forms.formsets.BaseFormSet.can_delete_extra) for more information.
			- [BaseFormSet](https://docs.djangoproject.com/en/4.2/topics/forms/formsets/#django.forms.formsets.BaseFormSet) now reports a user facing error, rather than raising an exception, when the management form is missing or has been tampered with. To customize this error message, pass the error_messages argument with the key 'missing_management_form' when instantiating the formset.
		- #### Generic Views [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#generic-views)
			- The week_format attributes of [WeekMixin](https://docs.djangoproject.com/en/4.2/ref/class-based-views/mixins-date-based/#django.views.generic.dates.WeekMixin) and [WeekArchiveView](https://docs.djangoproject.com/en/4.2/ref/class-based-views/generic-date-based/#django.views.generic.dates.WeekArchiveView) now support the '%V' ISO 8601 week format.
		- #### Management Commands [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#management-commands)
			- [loaddata](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-loaddata) now supports fixtures stored in XZ archives (.xz) and LZMA archives (.lzma).
			- [dumpdata](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-dumpdata) now can compress data in the bz2, gz, lzma, or xz formats.
			- [makemigrations](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-makemigrations) can now be called without an active database connection. In that case, check for a consistent migration history is skipped.
			- [BaseCommand.requires_system_checks](https://docs.djangoproject.com/en/4.2/howto/custom-management-commands/#django.core.management.BaseCommand.requires_system_checks) now supports specifying a list of tags. System checks registered in the chosen tags will be checked for errors prior to executing the command. In previous versions, either all or none of the system checks were performed.
			- Support for colored terminal output on Windows is updated. Various modern terminal environments are automatically detected, and the options for enabling support in other cases are improved. See [Syntax coloring](https://docs.djangoproject.com/en/4.2/ref/django-admin/#syntax-coloring) for more details.
		- #### Migrations [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#migrations)
			- The new Operation.migration_name_fragment property allows providing a filename fragment that will be used to name a migration containing only that operation.
			- Migrations now support serialization of pure and concrete path objects from [pathlib](https://docs.python.org/3/library/pathlib.html#module-pathlib), and [os.PathLike](https://docs.python.org/3/library/os.html#os.PathLike) instances.
		- #### Models [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#models)
			- The new no_key parameter for [QuerySet.select_for_update()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.select_for_update), supported on PostgreSQL, allows acquiring weaker locks that don’t block the creation of rows that reference locked rows through a foreign key.
			- [When()](https://docs.djangoproject.com/en/4.2/ref/models/conditional-expressions/#django.db.models.expressions.When) expression now allows using the condition argument with lookups.
			- The new [Index.include](https://docs.djangoproject.com/en/4.2/ref/models/indexes/#django.db.models.Index.include) and [UniqueConstraint.include](https://docs.djangoproject.com/en/4.2/ref/models/constraints/#django.db.models.UniqueConstraint.include) attributes allow creating covering indexes and covering unique constraints on PostgreSQL 11+.
			- The new [UniqueConstraint.opclasses](https://docs.djangoproject.com/en/4.2/ref/models/constraints/#django.db.models.UniqueConstraint.opclasses) attribute allows setting PostgreSQL operator classes.
			- The [QuerySet.update()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.update) method now respects the order_by() clause on MySQL and MariaDB.
			- [FilteredRelation()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.FilteredRelation) now supports nested relations.
			- The of argument of [QuerySet.select_for_update()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.select_for_update) is now allowed on MySQL 8.0.1+.
			- [Value()](https://docs.djangoproject.com/en/4.2/ref/models/expressions/#django.db.models.Value) expression now automatically resolves its output_field to the appropriate [Field](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.Field) subclass based on the type of its provided value for [bool](https://docs.python.org/3/library/functions.html#bool), [bytes](https://docs.python.org/3/library/stdtypes.html#bytes), [float](https://docs.python.org/3/library/functions.html#float), [int](https://docs.python.org/3/library/functions.html#int), [str](https://docs.python.org/3/library/stdtypes.html#str), [datetime.date](https://docs.python.org/3/library/datetime.html#datetime.date), [datetime.datetime](https://docs.python.org/3/library/datetime.html#datetime.datetime), [datetime.time](https://docs.python.org/3/library/datetime.html#datetime.time), [datetime.timedelta](https://docs.python.org/3/library/datetime.html#datetime.timedelta), [decimal.Decimal](https://docs.python.org/3/library/decimal.html#decimal.Decimal), and [uuid.UUID](https://docs.python.org/3/library/uuid.html#uuid.UUID) instances. As a consequence, resolving an output_field for database functions and combined expressions may now crash with mixed types when using Value(). You will need to explicitly set the output_field in such cases.
			- The new [QuerySet.alias()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.alias) method allows creating reusable aliases for expressions that don’t need to be selected but are used for filtering, ordering, or as a part of complex expressions.
			- The new [Collate](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.Collate) function allows filtering and ordering by specified database collations.
			- The field_name argument of [QuerySet.in_bulk()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.in_bulk) now accepts distinct fields if there’s only one field specified in [QuerySet.distinct()](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#django.db.models.query.QuerySet.distinct).
			- The new tzinfo parameter of the [TruncDate](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.TruncDate) and [TruncTime](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.TruncTime) database functions allows truncating datetimes in a specific timezone.
			- The new db_collation argument for [CharField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.CharField.db_collation) and [TextField](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.TextField.db_collation) allows setting a database collation for the field.
			- Added the [Random](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.Random) database function.
			- [Aggregation functions](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#aggregation-functions), [F()](https://docs.djangoproject.com/en/4.2/ref/models/expressions/#django.db.models.F), [OuterRef()](https://docs.djangoproject.com/en/4.2/ref/models/expressions/#django.db.models.OuterRef), and other expressions now allow using transforms. See [Expressions can reference transforms](https://docs.djangoproject.com/en/4.2/topics/db/queries/#using-transforms-in-expressions) for details.
			- The new durable argument for [atomic()](https://docs.djangoproject.com/en/4.2/topics/db/transactions/#django.db.transaction.atomic) guarantees that changes made in the atomic block will be committed if the block exits without errors. A nested atomic block marked as durable will raise a RuntimeError.
			- Added the [JSONObject](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.JSONObject) database function.
		- #### Pagination [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#pagination)
			- The new [django.core.paginator.Paginator.get_elided_page_range()](https://docs.djangoproject.com/en/4.2/ref/paginator/#django.core.paginator.Paginator.get_elided_page_range) method allows generating a page range with some of the values elided. If there are a large number of pages, this can be helpful for generating a reasonable number of page links in a template.
		- #### Requests and Responses [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#requests-and-responses)
			- Response headers are now stored in [HttpResponse.headers](https://docs.djangoproject.com/en/4.2/ref/request-response/#django.http.HttpResponse.headers). This can be used instead of the original dict-like interface of HttpResponse objects. Both interfaces will continue to be supported. See [Setting header fields](https://docs.djangoproject.com/en/4.2/ref/request-response/#setting-header-fields) for details.
			- The new headers parameter of [HttpResponse](https://docs.djangoproject.com/en/4.2/ref/request-response/#django.http.HttpResponse), [SimpleTemplateResponse](https://docs.djangoproject.com/en/4.2/ref/template-response/#django.template.response.SimpleTemplateResponse), and [TemplateResponse](https://docs.djangoproject.com/en/4.2/ref/template-response/#django.template.response.TemplateResponse) allows setting response [headers](https://docs.djangoproject.com/en/4.2/ref/request-response/#django.http.HttpResponse.headers) on instantiation.
		- #### Security [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#security)
			- The [SECRET_KEY](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-SECRET_KEY) setting is now checked for a valid value upon first access, rather than when settings are first loaded. This enables running management commands that do not rely on the SECRET_KEY without needing to provide a value. As a consequence of this, calling [configure()](https://docs.djangoproject.com/en/4.2/topics/settings/#django.conf.settings.configure) without providing a valid SECRET_KEY, and then going on to access settings.SECRET_KEY will now raise an [ImproperlyConfigured](https://docs.djangoproject.com/en/4.2/ref/exceptions/#django.core.exceptions.ImproperlyConfigured) exception.
			- The new Signer.sign_object() and Signer.unsign_object() methods allow signing complex data structures. See [Protecting complex data structures](https://docs.djangoproject.com/en/4.2/topics/signing/#signing-complex-data) for more details.
			- Also, [signing.dumps()](https://docs.djangoproject.com/en/4.2/topics/signing/#django.core.signing.dumps) and [loads()](https://docs.djangoproject.com/en/4.2/topics/signing/#django.core.signing.loads) become shortcuts for [TimestampSigner.sign_object()](https://docs.djangoproject.com/en/4.2/topics/signing/#django.core.signing.TimestampSigner.sign_object) and [unsign_object()](https://docs.djangoproject.com/en/4.2/topics/signing/#django.core.signing.TimestampSigner.unsign_object).
		- #### Serialization [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#serialization)
			- The new [JSONL](https://docs.djangoproject.com/en/4.2/topics/serialization/#serialization-formats-jsonl) serializer allows using the JSON Lines format with [dumpdata](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-dumpdata) and [loaddata](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-loaddata). This can be useful for populating large databases because data is loaded line by line into memory, rather than being loaded all at once.
		- #### Signals [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#signals)
			- [Signal.send_robust()](https://docs.djangoproject.com/en/4.2/topics/signals/#django.dispatch.Signal.send_robust) now logs exceptions.
		- #### Templates [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#templates)
			- [floatformat](https://docs.djangoproject.com/en/4.2/ref/templates/builtins/#std-templatefilter-floatformat) template filter now allows using the g suffix to force grouping by the [THOUSAND_SEPARATOR](https://docs.djangoproject.com/en/4.2/ref/settings/#std-setting-THOUSAND_SEPARATOR) for the active locale.
			- Templates cached with [Cached template loaders](https://docs.djangoproject.com/en/4.2/ref/templates/api/#template-loaders) are now correctly reloaded in development.
		- #### Tests [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#tests)
			- Objects assigned to class attributes in [TestCase.setUpTestData()](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.TestCase.setUpTestData) are now isolated for each test method. Such objects are now required to support creating deep copies with [copy.deepcopy()](https://docs.python.org/3/library/copy.html#copy.deepcopy). Assigning objects which don’t support deepcopy() is deprecated and will be removed in Django 4.1.
			- [DiscoverRunner](https://docs.djangoproject.com/en/4.2/topics/testing/advanced/#django.test.runner.DiscoverRunner) now enables [faulthandler](https://docs.python.org/3/library/faulthandler.html#module-faulthandler) by default. This can be disabled by using the [test --no-faulthandler](https://docs.djangoproject.com/en/4.2/ref/django-admin/#cmdoption-test-no-faulthandler) option.
			- [DiscoverRunner](https://docs.djangoproject.com/en/4.2/topics/testing/advanced/#django.test.runner.DiscoverRunner) and the [test](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-test) management command can now track timings, including database setup and total run time. This can be enabled by using the [test --timing](https://docs.djangoproject.com/en/4.2/ref/django-admin/#cmdoption-test-timing) option.
			- [Client](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.Client) now preserves the request query string when following 307 and 308 redirects.
			- The new [TestCase.captureOnCommitCallbacks()](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.TestCase.captureOnCommitCallbacks) method captures callback functions passed to [transaction.on_commit()](https://docs.djangoproject.com/en/4.2/topics/db/transactions/#django.db.transaction.on_commit) in a list. This allows you to test such callbacks without using the slower [TransactionTestCase](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.TransactionTestCase).
			- [TransactionTestCase.assertQuerysetEqual()](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.TransactionTestCase.assertQuerySetEqual) now supports direct comparison against another queryset rather than being restricted to comparison against a list of string representations of objects when using the default value for the transform argument.
		- #### Utilities [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#utilities)
			- The new depth parameter of django.utils.timesince.timesince() and django.utils.timesince.timeuntil() functions allows specifying the number of adjacent time units to return.
		- #### Validators [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#validators)
			- Built-in validators now include the provided value in the params argument of a raised [ValidationError](https://docs.djangoproject.com/en/4.2/ref/exceptions/#django.core.exceptions.ValidationError). This allows custom error messages to use the %(value)s placeholder.
			- The [ValidationError](https://docs.djangoproject.com/en/4.2/ref/exceptions/#django.core.exceptions.ValidationError) equality operator now ignores messages and params ordering.
		- ## Backwards incompatible changes in 3.2 [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#backwards-incompatible-changes-in-3-2)
			- ### Database backend API [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#database-backend-api)
				- This section describes changes that may be needed in third-party database backends.
					- The new DatabaseFeatures.introspected_field_types property replaces these features:
						- can_introspect_autofield
						- can_introspect_big_integer_field
						- can_introspect_binary_field
						- can_introspect_decimal_field
						- can_introspect_duration_field
						- can_introspect_ip_address_field
						- can_introspect_positive_integer_field
						- can_introspect_small_integer_field
						- can_introspect_time_field
						- introspected_big_auto_field_type
						- introspected_small_auto_field_type
						- introspected_boolean_field_type
				- To enable support for covering indexes ([Index.include](https://docs.djangoproject.com/en/4.2/ref/models/indexes/#django.db.models.Index.include)) and covering unique constraints ([UniqueConstraint.include](https://docs.djangoproject.com/en/4.2/ref/models/constraints/#django.db.models.UniqueConstraint.include)), set DatabaseFeatures.supports_covering_indexes to True.
				- Third-party database backends must implement support for column database collations on CharFields and TextFields or set DatabaseFeatures.supports_collation_on_charfield and DatabaseFeatures.supports_collation_on_textfield to False. If non-deterministic collations are not supported, set supports_non_deterministic_collations to False.
				- DatabaseOperations.random_function_sql() is removed in favor of the new [Random](https://docs.djangoproject.com/en/4.2/ref/models/database-functions/#django.db.models.functions.Random) database function.
				- DatabaseOperations.date_trunc_sql() and DatabaseOperations.time_trunc_sql() now take the optional tzname argument in order to truncate in a specific timezone.
				- DatabaseClient.runshell() now gets arguments and an optional dictionary with environment variables to the underlying command-line client from DatabaseClient.settings_to_cmd_args_env() method. Third-party database backends must implement DatabaseClient.settings_to_cmd_args_env() or override DatabaseClient.runshell().
				- Third-party database backends must implement support for functional indexes ([Index.expressions](https://docs.djangoproject.com/en/4.2/ref/models/indexes/#django.db.models.Index.expressions)) or set DatabaseFeatures.supports_expression_indexes to False. If COLLATE is not a part of the CREATE INDEX statement, set DatabaseFeatures.collate_as_index_expression to True.
		- ### [django.contrib.admin](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#module-django.contrib.admin) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#id1)
			- Pagination links in the admin are now 1-indexed instead of 0-indexed, i.e. the query string for the first page is ?p=1 instead of ?p=0.
			- The new admin catch-all view will break URL patterns routed after the admin URLs and matching the admin URL prefix. You can either adjust your URL ordering or, if necessary, set [AdminSite.final_catch_all_view](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.AdminSite.final_catch_all_view) to False, disabling the catch-all view. See [What’s new in Django 3.2](https://docs.djangoproject.com/en/4.2/releases/3.2/#whats-new-3-2) for more details.
			- Minified JavaScript files are no longer included with the admin. If you require these files to be minified, consider using a third party app or external build tool. The minified vendored JavaScript files packaged with the admin (e.g. [jquery.min.js](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#contrib-admin-jquery)) are still included.
			- [ModelAdmin.prepopulated_fields](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#django.contrib.admin.ModelAdmin.prepopulated_fields) no longer strips English stop words, such as 'a' or 'an'.
		- ### [django.contrib.gis](https://docs.djangoproject.com/en/4.2/ref/contrib/gis/#module-django.contrib.gis) [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#id2)
			- Support for PostGIS 2.2 is removed.
			- The Oracle backend now clones polygons (and geometry collections containing polygons) before reorienting them and saving them to the database. They are no longer mutated in place. You might notice this if you use the polygons after a model is saved.
		- ### Dropped support for PostgreSQL 9.5 [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#dropped-support-for-postgresql-9-5)
			- Upstream support for PostgreSQL 9.5 ends in February 2021. Django 3.2 supports PostgreSQL 9.6 and higher.
		- ### Dropped support for MySQL 5.6 [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#dropped-support-for-mysql-5-6)
			- The end of upstream support for MySQL 5.6 is April 2021. Django 3.2 supports MySQL 5.7 and higher.
		- ### Miscellaneous [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#miscellaneous)
			- Django now supports non-pytz time zones, such as Python 3.9+’s [zoneinfo](https://docs.python.org/3/library/zoneinfo.html#module-zoneinfo) module and its backport.
			- The undocumented SpatiaLiteOperations.proj4_version() method is renamed to proj_version().
			- [slugify()](https://docs.djangoproject.com/en/4.2/ref/utils/#django.utils.text.slugify) now removes leading and trailing dashes and underscores.
			- The [intcomma](https://docs.djangoproject.com/en/4.2/ref/contrib/humanize/#std-templatefilter-intcomma) and [intword](https://docs.djangoproject.com/en/4.2/ref/contrib/humanize/#std-templatefilter-intword) template filters no longer depend on the USE_L10N setting.
			- Support for argon2-cffi < 19.1.0 is removed.
			- The cache keys no longer includes the language when internationalization is disabled (USE_I18N = False) and localization is enabled (USE_L10N = True). After upgrading to Django 3.2 in such configurations, the first request to any previously cached value will be a cache miss.
			- ForeignKey.validate() now uses [_base_manager](https://docs.djangoproject.com/en/4.2/topics/db/managers/#django.db.models.Model._base_manager) rather than [_default_manager](https://docs.djangoproject.com/en/4.2/topics/db/managers/#django.db.models.Model._default_manager) to check that related instances exist.
			- When an application defines an [AppConfig](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig) subclass in an apps.py submodule, Django now uses this configuration automatically, even if it isn’t enabled with default_app_config. Set default = False in the [AppConfig](https://docs.djangoproject.com/en/4.2/ref/applications/#django.apps.AppConfig) subclass if you need to prevent this behavior. See [What’s new in Django 3.2](https://docs.djangoproject.com/en/4.2/releases/3.2/#whats-new-3-2) for more details.
			- Instantiating an abstract model now raises TypeError.
			- Keyword arguments to [setup_databases()](https://docs.djangoproject.com/en/4.2/topics/testing/advanced/#django.test.utils.setup_databases) are now keyword-only.
			- The undocumented django.utils.http.limited_parse_qsl() function is removed. Please use [urllib.parse.parse_qsl()](https://docs.python.org/3/library/urllib.parse.html#urllib.parse.parse_qsl) instead.
			- django.test.utils.TestContextDecorator now uses [addCleanup()](https://docs.python.org/3/library/unittest.html#unittest.TestCase.addCleanup) so that cleanups registered in the [setUp()](https://docs.python.org/3/library/unittest.html#unittest.TestCase.setUp) method are called before TestContextDecorator.disable().
			- SessionMiddleware now raises a [SessionInterrupted](https://docs.djangoproject.com/en/4.2/ref/exceptions/#django.contrib.sessions.exceptions.SessionInterrupted) exception instead of [SuspiciousOperation](https://docs.djangoproject.com/en/4.2/ref/exceptions/#django.core.exceptions.SuspiciousOperation) when a session is destroyed in a concurrent request.
			- The [django.db.models.Field](https://docs.djangoproject.com/en/4.2/ref/models/fields/#django.db.models.Field) equality operator now correctly distinguishes inherited field instances across models. Additionally, the ordering of such fields is now defined.
			- The undocumented django.core.files.locks.lock() function now returns False if the file cannot be locked, instead of raising [BlockingIOError](https://docs.python.org/3/library/exceptions.html#BlockingIOError).
			- The password reset mechanism now invalidates tokens when the user email is changed.
			- [makemessages](https://docs.djangoproject.com/en/4.2/ref/django-admin/#django-admin-makemessages) command no longer processes invalid locales specified using [makemessages --locale](https://docs.djangoproject.com/en/4.2/ref/django-admin/#cmdoption-makemessages-locale) option, when they contain hyphens ('-').
			- The django.contrib.auth.forms.ReadOnlyPasswordHashField form field is now [disabled](https://docs.djangoproject.com/en/4.2/ref/forms/fields/#django.forms.Field.disabled) by default. Therefore UserChangeForm.clean_password() is no longer required to return the initial value.
			- The cache.get_many(), get_or_set(), has_key(), incr(), decr(), incr_version(), and decr_version() cache operations now correctly handle None stored in the cache, in the same way as any other value, instead of behaving as though the key didn’t exist.
			- Due to a python-memcached limitation, the previous behavior is kept for the deprecated MemcachedCache backend.
			- The minimum supported version of SQLite is increased from 3.8.3 to 3.9.0.
			- [CookieStorage](https://docs.djangoproject.com/en/4.2/ref/contrib/messages/#django.contrib.messages.storage.cookie.CookieStorage) now stores messages in the [**RFC 6265**](https://datatracker.ietf.org/doc/html/rfc6265.html) compliant format. Support for cookies that use the old format remains until Django 4.1.
			- The minimum supported version of asgiref is increased from 3.2.10 to 3.3.2.
		- ## Features deprecated in 3.2 [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#features-deprecated-in-3-2)
			- ### Miscellaneous [¶](https://docs.djangoproject.com/en/4.2/releases/3.2/#id3)
		- Assigning objects which don’t support creating deep copies with [copy.deepcopy()](https://docs.python.org/3/library/copy.html#copy.deepcopy) to class attributes in [TestCase.setUpTestData()](https://docs.djangoproject.com/en/4.2/topics/testing/tools/#django.test.TestCase.setUpTestData) is deprecated.
		- Using a boolean value in [BaseCommand.requires_system_checks](https://docs.djangoproject.com/en/4.2/howto/custom-management-commands/#django.core.management.BaseCommand.requires_system_checks) is deprecated. Use '__all__' instead of True, and [] (an empty list) instead of False.
		- The whitelist argument and domain_whitelist attribute of [EmailValidator](https://docs.djangoproject.com/en/4.2/ref/validators/#django.core.validators.EmailValidator) are deprecated. Use allowlist instead of whitelist, and domain_allowlist instead of domain_whitelist. You may need to rename whitelist in existing migrations.
		- The default_app_config application configuration variable is deprecated, due to the now automatic AppConfig discovery. See [What’s new in Django 3.2](https://docs.djangoproject.com/en/4.2/releases/3.2/#whats-new-3-2) for more details.
		- Automatically calling repr() on a queryset in TransactionTestCase.assertQuerysetEqual(), when compared to string values, is deprecated. If you need the previous behavior, explicitly set transform to repr.
		- The django.core.cache.backends.memcached.MemcachedCache backend is deprecated as python-memcached has some problems and seems to be unmaintained. Use django.core.cache.backends.memcached.PyMemcacheCache or django.core.cache.backends.memcached.PyLibMCCache instead.
		- The format of messages used by django.contrib.messages.storage.cookie.CookieStorage is different from the format generated by older versions of Django. Support for the old format remains until Django 4.1.
-