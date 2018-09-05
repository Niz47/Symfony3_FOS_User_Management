---
name: override twig template err in symfony 3
about: 'Suggest an idea '

---

I use sonata admin 3 for my symfony-3 project. I'm facing with twig template error as below.

*Error number 1*

> [2018-09-05 03:02:14] request.CRITICAL: Uncaught PHP Exception
> Twig_Error_Loader: "Unable to find template
> "AppBundle:Admin:user_block.html.twig" (looked into:
> /var/www/mypay-portal/vendor/knplabs/knp-menu/src/Knp/Menu/Resources/views,
> /var/www/mypay-portal/app/Resources/views,
> /var/www/mypay-portal/vendor/symfony/symfony/src/Symfony/Bridge/Twig/Resources/views/Form)
> in "SonataAdminBundle::standard_layout.html.twig" at line 215." at
> /var/www/mypay-portal/vendor/twig/twig/lib/Twig/Loader/Filesystem.php
> line 232 {"exception":"[object] (Twig_Error_Loader(code: 0): Unable to
> find template \"AppBundle:Admin:user_block.html.twig\" (looked into:
> /var/www/mypay-portal/vendor/knplabs/knp-menu/src/Knp/Menu/Resources/views,
> /var/www/mypay-portal/app/Resources/views,
> /var/www/mypay-portal/vendor/symfony/symfony/src/Symfony/Bridge/Twig/Resources/views/Form)
> in \"SonataAdminBundle::standard_layout.html.twig\" at line 215. at
> /var/www/mypay-portal/vendor/twig/twig/lib/Twig/Loader/Filesystem.php:232)"}
> []

----
In `config/config.yml`

    sonata_admin:
        title: MyPay Admin
        title_logo: bundles/app/images/logo.png
        templates:
            user_block: AppBundle:Admin:user_block.html.twig


------

*Error number 2*


> [2018-09-05 03:40:28] app.WARNING: An error occured trying to load the
> template "AppBundle:Admin:date_format_list.html.twig" for the field
> "created_date_time", the default template
> "@SonataAdmin/CRUD/base_list_field.html.twig" was used instead.
> {"exception":"[object] (Twig_Error_Loader(code: 0): Unable to find
> template \"AppBundle:Admin:date_format_list.html.twig\" (looked into:
> /var/www/mypay-portal/vendor/knplabs/knp-menu/src/Knp/Menu/Resources/views,
> /var/www/mypay-portal/app/Resources/views,
> /var/www/mypay-portal/vendor/symfony/symfony/src/Symfony/Bridge/Twig/Resources/views/Form).
> at
> /var/www/mypay-portal/vendor/twig/twig/lib/Twig/Loader/Filesystem.php:232)"}
> []

In `AppBundle/Admin/ProviderAdmin.php`
__________________________________

    $listMapper
                ->addIdentifier('id')
                ->add('providerId')
                ->add('providerName')
                ->add(
                    'created_date_time',
                    'datetime',
                    ['template' => 'AppBundle:Admin:date_format_list.html.twig']
                )
                ->add(
                    '_action',
                    'actions',
                    ['actions' => ['show' => [], 'edit' => []]]
                );

--------

In `AppBundle/Resources/Views/Admin/date_format_list.html.twig`

    <td>
        {%  if value is  not empty %}
            {{  value | to_MMT }}
        {%  else %}
            {{ value }}
        {% endif %}
    </td>

It happened from this admin >> The server returned a "`500 Internal Server Error`". How can I fix this?
