BitrixSnippets - Набор сниппетов для CMS Bitrix
==============================
####Набор делался для внутреннего использования, но вдруг кому-то ещё он пригодится.

Оригинальная идея и скрипт генерации сниппетов взят из [этой ветки][1] и немного доработан так, чтобы генерировать более юзабельные сниппеты.

####В наборе пока только сниппеты основных компонентов bitrix.
Для вставки сниппета достаточно написать `bx_` и появится окошко автокомплита.
Для корректной работы сниппетов все точки в названиях компонентов заменены на `_`, таким образом для вставки компонента `bitrix:news.list` можно прописать `bx_news_list`.

####Список кастомных сниппетов
Сниппеты, добавленный вручную:
*bx_add_head_script*
```
<?$APPLICATION->AddHeadScript(SITE_TEMPLATE_PATH.'/js/main.js', true)?>
```
*bx_first*
```
<?if(!defined("B_PROLOG_INCLUDED") || B_PROLOG_INCLUDED!==true)die();
IncludeTemplateLangFile(__FILE__);
$CurPage = $APPLICATION->GetCurPage();
?>
```
*bx_getcurpage*
```
$APPLICATION->GetCurPage()
```
*bx_inc_1*
```
<?$APPLICATION->IncludeComponent("bitrix:main.include", ".default", array(
	"AREA_FILE_SHOW" => "file",
	"PATH" => "/local/codenails/includes/file.php",
	"EDIT_TEMPLATE" => ""
	),
	false
);?>
```
*bx_isadmin*
```
<?
global $USER;
if ($USER->IsAdmin()) {
	
};
?>
```
*bx_lang*
```
<?=LANGUAGE_ID?>
```
*bx_printr*
```
<?echo "<pre class='cn-pre' data-text='arResult'>"; print_r($arResult); echo "</pre>";?>
```
*bx_set_additional_css*
```
<?$APPLICATION->SetAdditionalCSS(SITE_TEMPLATE_PATH.'/css/main.css', true)?>
```
*bx_set_description*
```
<?
	$ShortText = htmlspecialchars(strip_tags(stripslashes($arResult["DETAIL_TEXT"])));

	if (strlen($ShortText) > 200) {
		$ShortText = substr($ShortText, 0, 200);					
		if($word_pos = strrpos($ShortText, ' ')) $ShortText = substr($ShortText, 0, $word_pos);			
	} 
	$APPLICATION->SetPageProperty("description", $ShortText);
?>
```
*bx_showhead*
```
<?$APPLICATION->ShowHead();?>
```
*bx_showpanel*
```
<?$APPLICATION->ShowPanel();?>
```
*bx_showtitle*
```
<?$APPLICATION->ShowTitle(false)?>
```
*bx_template*
```
<?=SITE_TEMPLATE_PATH?>/
```


*bx_resize_image_get*
```
<?
	// Ресайз картинки для последующего показа через MagnificPopup
	$image = CFile::ResizeImageGet($arResult['DETAIL_PICTURE'], array('width'=>150, 'height'=>150), BX_RESIZE_IMAGE_PROPORTIONAL_ALT, true);
	$resizedImg = ($image['src']) ? $image['src'] : $arResult['DETAIL_PICTURE'];
?>
<img 
	class="popup-image" 
	src="<?=$resizedImg?>" 
	data-mfp-src="<?=$arResult['DETAIL_PICTURE']['SRC']?>"
	alt="<?=$arResult['DETAIL_PICTURE']['ALT']?>"
	title="<?=$arResult['DETAIL_PICTURE']['TITLE']?>"
>
// Вставка в js-файл
// Галерея картинок
$('.popup-image').magnificPopup({
	type: 'image',
	gallery: {
		enabled: true
	}
});
```

*bx_composite_js*
``` javascript
if (window.frameCacheVars !== undefined) {
    BX.addCustomEvent("onFrameDataReceived", function (json) {
        runFunction();
    });
}
else {
    jQuery(document).ready(function (\$) {
        runFunction();
    });
}

function runFunction() {
    ${0:console.log('go-go-go');}
}
```

*bxPrintr* Новый, более удобный *bx_printr* для последней версии быстрого старта.
```
<?bxPrintr(${1:/$arResult}, ${2:false}, '${3:arResult}');?>
${0}
```

  [1]: https://github.com/AndreyGo/SublimeBitrixSnippets
