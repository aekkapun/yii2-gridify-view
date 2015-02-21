# yii2-gridify

This is widget extended of ListView with plugin of https://github.com/hongkhanh/gridify. This widget allows load content automatically via Ajax when you reach the end of the page. Content is displayed in table form.

# How use

Added in your controller following code:

```php
public function actionIndex()
{
    $searchModel = new ModelSearch();
    $dataProvider = $searchModel->search(Yii::$app->request->queryParams);

    if (Yii::$app->request->isAjax) {
        return $this->renderPartial('_page', [
            'dataProvider' => $dataProvider,
            'onlyItems' => true,
        ]);
    }

    return $this->render('index', [
        'dataProvider' => $dataProvider,
        'searchModel' => $searchModel,
    ]);
}
```

Added in your ```index``` view following code:

```php
$this->render('_page', [
    'dataProvider' => $dataProvider,
]);
```

Added in your ```_page``` view following code:

```php
use bupy7\gridifyview\GridifyView;

echo GridifyView::widget([
    'dataProvider' => $dataProvider,
    'itemView' => '_item',
    'onlyItems' => isset($onlyItems) ? $onlyItems : false,
    'pluginOptions' => [
        'url' => ['/path/to/actin/in/your/controller'],
        'srcNode' => '> div',
        'resizable' => true,
        'width' => '250px',
        'maxWidth' => '350px',
        'margin' => '20px',
    ],
]);
```

# License

