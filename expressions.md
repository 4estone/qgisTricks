#### Get size of SVG in Python
```python 
xml.etree.ElementTree.parse(sl.path()).getroot().attrib["width"]
```


#### Limiter les choix d'une liste selon l'emprise

Type de champ  "Valeur relationnelle"

  ``intersects(  $geometry ,  geomFromWKT( $current_canvas_extent ))`` 

A partir de la 2.18

  ``intersects(  $geometry ,  geomFromWKT(current_canvas_extent()))`` 

La fonction:
```python
from qgis.utils import qgsfunction
from qgis.utils import iface
	
@qgsfunction(0, "Python")
def current_canvas_extent(values, feature, parent)
""" 
	       retourne l etendue courante de la carte
""" 
    extend = iface.mapCanvas().extent().asWktPolygon() 
    return extend
```


#### Récupérer l'objet Layer
```python
lyr = [l for l in layers if l.name() == u'my_layer_name'][0]
pr = lyr.dataProvider()
```

#### Générer des qml pour toutes les layers
```python
for layer in QgsMapLayerRegistry.instance().mapLayers().values():
    layer.saveNamedStyle(layer.source()[:-4] + '.qml')
```


#### Extraction coordonnées lat/long
```python
x(transform( $geometry , 'EPSG:3948', 'EPSG:4326' ) )
y(transform( $geometry , 'EPSG:3948', 'EPSG:4326' ) )
```

#### script de paramétrage formulaire
	Les formulaires QGIS peuvent avoir une fonction Python qui sera appelée à l'ouverture du formulaire.
	
	Utilisez cette fonction pour ajouter plus de fonctionnalités à vos formulaires.
	
	Entrez le nom de la fonction dans le champ
	"Fonction d'initialisation Python"
```python
# -*- coding: utf-8 -*-
from PyQt4.QtGui import QWidget
	
def my_form_open(dialog, layer, feature):
   geom = feature.geometry()
   control = dialog.findChild(QWidget, "MyLineEdit")``
```


	
#### Générer ligne

``st_linestringfromtext('linestring (' || coord || ')', 2154) ``
	
au lieu de 
	
``st_linestringfromtext('linestring (coord)', 2154) ``

 coord sera interprété comme un nom de champ et pas comme une chaîne de caractères 
	

