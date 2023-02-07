# Modificări

Aici se va ține evidența modificărilor făcute asupra template-ului Default pentru a realiza versiunea nipne.

## Versiunea 0.0.2

A fost adus fișierul din `/application/view/site/item/browse.phtml` în `themes/nipne/view/omeka/site/item/browse.phtml`.

A fost modificată sursa la foreach-ul care afișează un set de n resurse în zona de răsfoire (browse) a acestora. Codul modificat este marcat cu un comentariu `mod nipne`.

```php
foreach ($items as $item):
    $heading = $headingTerm ? $item->value($headingTerm, ['default' => $translate('[Untitled]'), 'lang' => ($filterLocale ? [$lang, ''] : null)]) : $item->displayTitle(null, ($filterLocale ? [$lang, ''] : null));
    $body = $bodyTerm ? $item->value($bodyTerm, ['lang' => ($filterLocale ? [$lang, ''] : null)]) : $item->displayDescription(null, ($filterLocale ? [$lang, ''] : null));
    // nipne mod
    $creators = $item->value('dcterms:creator');
    $editors = $item->value('dcterms:editor');
    $responsables = $creators ? $creators : $editors;
?>
    <li class="item resource">
        <?php // echo $item->linkPretty('medium', $heading); ?>
        
        <?php 
			// nipne mod
			if ($itemThumbnail = $this->thumbnail($item, 'medium')): 
			 echo $item->linkRaw($itemThumbnail);
			endif; 
		?>
        <h4><?php echo $item->link($heading); ?></h4>
		<p><?php echo $responsables; ?></p>
        
        <?php if ($body): ?>
			<div class="description"><?php echo $escape($body); ?></div>
        <?php endif; ?>
    </li>
<?php endforeach; ?>
```
