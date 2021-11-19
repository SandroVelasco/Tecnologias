## Estrutura de um módulo
- Pasta mãe
- Pasta filho (nome do módulo)

Exemplo:
app/code/Pasta mãe/Pasta filho
app/code/Synapcom/CreatedAtFormatted

## Passos
1. Criar pasta com nome do módulo
2. Inserir arquivo registration.php
```php
<?php

\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'Synapcom_CreatedAtFormatted',
    __DIR__
);
```
3. Inserir arquivo di.xml em /etc (CreatedAtFormatted/etc/di.xml)
```php
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <preference for="Magento\Sales\Model\Order" type="Synapcom\CreatedAtFormatted\Model\Rewrite\Order" />
</config>
```
4. Inserir arquivo module.xml em /etc (CreatedAtFormatted/etc/module.xml)
```php
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="Synapcom_CreatedAtFormatted" />
</config>
```
5. Criar pastas necessárias, como definidas acima (Model/Rewrite/Order.php)
```php
<?php

namespace Synapcom\CreatedAtFormatted\Model\Rewrite;

class Order extends \Magento\Sales\Model\Order
{
    public function getCreatedAtWithoutTime()
    {
        $date = new \DateTime($this->getCreatedAt());

        return $date->format('d/m/Y'); 
    }
}
```

Dessa forma, o método getCreatedAtWithoutTime será inserido na classe Order.