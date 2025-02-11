# Отозвать роль на ресурс

Вы можете запретить [субъекту](../../../iam/concepts/access-control/index.md#subject) доступ к ресурсу, для этого необходимо отозвать у него соответствующие [роли](../../../iam/concepts/access-control/roles.md) на этот ресурс и на ресурсы, от которых наследуются права доступа. Подробнее читайте в разделе [{#T}](../../../iam/concepts/access-control/index.md).

{% list tabs %}

- Консоль управления

  1. В [консоли управления]({{ link-console-main }}) выберите [каталог](../../../resource-manager/concepts/resources-hierarchy.md#folder), в котором нужно отозвать роль на ресурс.
  1. В списке сервисов выберите **{{ ui-key.yacloud.iam.folder.dashboard.label_container-registry }}**.
  1. Отзовите роль на ресурс.
     * Отозвать роль на реестр:
       1. Справа от имени нужного реестра нажмите значок ![horizontal-ellipsis](../../../_assets/horizontal-ellipsis.svg) и выберите **{{ ui-key.yacloud.cr.registry.overview.button_registry-acl }}**.
       1. В открывшемся окне в строке с именем пользователя, разрешения которого вы хотите отозвать, раскройте выпадающий список.
       1. Снимите отметку с роли, которую хотите отозвать.

          Чтобы отозвать все разрешения пользователя, нажмите кнопку **{{ ui-key.yacloud.component.acl-dialog.button_revoke }}**.
       1. Нажмите кнопку **{{ ui-key.yacloud.common.save }}**.
     * Отозвать роль на репозиторий:
       1. Выберите нужный реестр.
       1. Справа от имени нужного репозитория нажмите значок ![horizontal-ellipsis](../../../_assets/horizontal-ellipsis.svg) и выберите **{{ ui-key.yacloud.cr.registry.overview.button_repository-acl }}**.
       1. В открывшемся окне в строке с именем пользователя, разрешения которого вы хотите отозвать, раскройте выпадающий список.
       1. Снимите отметку с роли, которую хотите отозвать.

          Чтобы отозвать все разрешения пользователя, нажмите кнопку **{{ ui-key.yacloud.component.acl-dialog.button_revoke }}**.
       1. Нажмите кнопку **{{ ui-key.yacloud.common.save }}**.

- CLI

  {% include [cli-install](../../../_includes/cli-install.md) %}

  {% include [default-catalogue](../../../_includes/default-catalogue.md) %}

  1. Просмотрите назначенные роли:

     ```bash
     yc <имя сервиса> <ресурс> list-access-bindings <имя ресурса>|<id ресурса>
     ```

     Где:
     * `<имя сервиса>` — имя сервиса `container`.
     * `<ресурс>` — категория ресурса `registry` или `repository`.
     * `<имя ресурса>` — имя ресурса, на который назначается роль. Вы можете указать ресурс по имени или идентификатору.
     * `<id ресурса>` — идентификатор ресурса, на который назначается роль.

     >Пример. Просмотрите роли на реестр с идентификатором `crp0pmf1n68dh715tf02`:
     >
     >```bash
     >yc container registry list-access-bindings crp0pmf1n68dh715tf02
     >```
     >
     >Результат:
     >
     >```bash
     >+--------------------------+------------------+----------------------+
     >|         ROLE ID          |   SUBJECT TYPE   |      SUBJECT ID      |
     >+--------------------------+------------------+----------------------+
     >| container-registry.admin | federatedAccount | kolhpriseeioo9dc3v24 |
     >+--------------------------+------------------+----------------------+
     >```

  1. Отзовите роль:

          
     ```bash
     yc <имя сервиса> <ресурс> remove-access-binding <имя ресурса>|<id ресурса> \
       --role <id роли> \
       --subject userAccount:<id пользователя>
     ```
     


     Где:
     * `<имя сервиса>` — имя сервиса `container`.
     * `<ресурс>` — категория ресурса `registry` или `repository`.
     * `<имя ресурса>` — имя ресурса, для которого отзывается роль. Вы можете указать ресурс по имени или идентификатору.
     * `<id ресурса>` — идентификатор ресурса, для которого отзывается роль.
     * `<id роли>` — идентификатор роли.
     * `<id пользователя>` — идентификатор группы, пользователя или сервисного аккаунта, для которого отзывается роль.

     >Пример. Отзовите роль `container-registry.admin` на реестр с идентификатором `crp0pmf1n68dh715tf02` для пользователя с идентификатором `kolhpriseeioo9dc3v24`:
     >

     
     >```bash
     >yc container registry remove-access-binding crp0pmf1n68dh715tf02 \
     >  --role container-registry.admin \
     >  --subject userAccount:kolhpriseeioo9dc3v24
     >```



- API

  Просмотрите назначенные роли с помощью метода `listAccessBindings` для ресурсов `registry` и `repository`.

  Отзовите роль методом `updateAccessBindings` для ресурсов `registry` и `repository`.

{% endlist %}

Подробнее об управлении ролями читайте в [документации](../../../iam/concepts/index.md) {{ iam-full-name }}.