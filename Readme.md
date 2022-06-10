# Comment utiliser un svg

## En passant par le fichier sprite.svg contenant plusieurs svg

Pour inclure un svg  
balise html svg  
balise html use  
attribut "xlink:href" avec le chemin du svg  
#+nom du svg dans le fichier svg (ils sont souvent plusieurs dans le même fichier)

svg class="search\_\_icon">  
 use xlink:href="img/sprite.svg#icon-magnifying-glass">/use>  
/svg>

---

# TIPS pour adapter la couleur d'un élément

## Dans le css on pose currentColor et l'élément aura automatiquement la couleur de l'élément ou de son parent. Très pratique par exemple ici sur une icon svg pour changer la couleur au hover

.icon {  
 width: 1.75rem;  
 height: 1.75rem;  
 margin-right: 2rem;  
 **fill: currentColor;**  
 }

---

# Rappel sélecteur CSS

## Quand on hover sur l'item, on fait quelque chose sur le before de cet item

.item:hover::before {  
 transform: scaleY(1);  
 }

---

# Poser trois (ou plus) effets de transition avec un délais

## On définit la transition sur trois actions : le transform (scaleY dessous) puis sur le width (toujours de dessous) MAIS avec un délais pour le width (la dernière propriété, le .2s) et le background color

.item::before {  
 transition: transform 0.2s, width .4s cubic-bezier(1, 0, 0, 1) .2s, background-color 0.1s;  
 }

.item:hover::before {  
 transform: scaleY(1);  
 width: 100%;  
 }

---

# Rappel sur le z-index : il ne fonctionne pas si l'élément ne possède pas une position (relative ou absolute ou fixed)

---

# Hack pour poser svg en CSS

## On peut poser un svg en CSS avec ::before en passant par background-image mais on ne pourra pas modifier sa couleur. Il existe maintenant une propriété "mask", qui permet de "voir" à travers un élément. Concrètement, on pose un background-color avec la couleur de svg, on pose la propriété "mask" qui prendre la forme du svg, laissera voir la couleur du background-color et cachera tout le reste. Ca donnera l'illusion d'avoir poser un svg de la bonne couleur. Encore en cours d'implémentation donc il faut ajouter wekbit devant la propriété

// old browser  
// background-image: url(../img/chevron-thin-right.svg);  
// background-size: cover;

// new browsers  
background-color: var(--color-primary);  
-webkit-mask-image: url(../img/chevron-thin-right.svg);  
-webkit-mask-size: cover;

---

# Responsive

## On ne peut pas utiliser les variables CSS dans les média queries, il faut passer par les variables SCSS

// 1200px / 16px  
$bp-largest: 75em;

@media only screen and ($bp-largest) {  
 }

---

# TIPS pour adapter la taille des images dans une grille

## Poser l'image dans un élément html, figure par exemple, puis utiliser object-fit sur l'image AVEC une width ET une height à 100%

section class="gallery">  
figure class="gallery\_\_item gallery\_\_item--1">  
img src="img/gal-1.jpeg" alt="Gallery image 1" class="gallery\_\_img" />  
/figure>  
/section>

.gallery\_\_img {  
width: 100%;  
height: 100%;  
object-fit: cover;  
display: block;  
}

---

# TIPS pour poser un overlay sur une background image

## Utiliser la propriété linear-gradient avec deux fois la même couleur puis l'image

.header {  
grid-column: full-start / col-end 6;  
background-image: linear-gradient(  
rgba($color-secondary, 0.93),  
      rgba($color-secondary, 0.93)  
),  
url(../img/hero.jpeg);  
background-size: cover;  
 background-position: center;  
}
