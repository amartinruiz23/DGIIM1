
Resumen Cálculo 

## Axiomas
- A1) Propiedad asociativa: `(x + y) + z = x + (y + z);	(xy)z = x(yz)`
- A2) Propiedad conmutativa: ` x + y = y + x; 		xy = yx`
- A3) Elemento neutro: `0 + x = x;		1x = x`
- A4) Elementos opuesto e inverso: `x + (-x) = 0; 		xx^(-1) = 1` 
- A5) Propiedad distributiva: `x(y + z) = xy + xz`
- A6) Ley de tricotomía: Solo puede pasar una de las tres siguientes: `x=0`, `x<0`, `x>0` 
- A7) Estabilidad de R+: Producto de positivos es siempre positivo
- A8) Axioma del continuo: Dados subconjuntos no vacíos A y B de números reales, tales que todo elemento de A <= todo elemento de B, se verifica que existe un número real z perteneciente a R, que es >= todo elemento de A y <= todo elemento de B (a<=z<=b)
	- Clave para demostrarlo: `{a>0, a²<=2}`, `{b>0, b²>=2}`; `a<=z<=b`. Se demuestra primero que no hay ningún racional cuyo cuadrado sea 2:
		-> Se prueba primero que no hay ningún número racional cuyo cuadrado es 2. 
		-> `r=m/n`; `m²=2n²` => `m` es par
		-> `m=2p`
		-> `n²=2p²` => `n` es par => no existe un número racional cuyo cuadrado es 2.
	- `0<=a²-b²` => `b+a>0` => `a<=b`
	- Demostrar la existencia de que hay un s que es mayor que r (s>r)
		-> Si `r<1` -> `s=1` => `1>=r`
		-> Tomar `E > 0`, que pertenezca a los reales positivos.

	
## Tema 1
- Axioma del continuo: Si `A` y `B` son conjuntos no vacíos de números reales, tales que todo número real de `A` es menor o igual que todo número de `B`, se verifica que hay algún número real que separa a ambos
- Principio del **supremo**
- Principio del **ínfimo**
- Intervalos
- Desigualdades y sus reglas

## Tema 2
- Conjunto de los números naturales `ℕ`
- Todo conjunto de números enteros y mayorado tiene máximo 
- Todo conjunto de números enteros y minorado tiene mínimo
- Todo conjunto de números naturales tiene mínimo
- Principio arquimediano del orden de los números reales `(ℕ no está mayorado en ℝ)`: para todo número real dado, siempre hay un natural mayor que él
- Función parte entera
- Potencias
- Dado un número a perteneciente a los positivos, existe un único número `b > 0`, cuya potencia `k` es igual a `a`: `b^k = a`. Se llama **"raíz k-ésima de a"**, `a^(1/k)`
- Un conjunto `A` es denso en un intervalo en `I` si, cada dos números de `I`, hay uno de `A`. Ejemplos: 
	- `Q` es denso en `ℝ`
	- `ℝ\Q` es denso en `R` 
- Desigualdad de las medias
- Finitud e infinitud
- Propiedades de los conjuntos finitos
	- Todo subconjunto de un finito es finito
	- Si `B` es un conjunto finito y `f:A->B` es una aplicación biyectiva -> `A es finito`
	- Si `A` es un conjunto finito y `g:A->B` es una aplicación sobreyectiva -> `B es finito`  
	- Todo conjunto finito y no vacío de números reales tiene máximo y mínimo
- Un conjunto se dice que es infinito cuando no es finito -> Si hay un conjunto sin máximos ni/o mínimos no puede ser finito
- Subconjuntos de `ℕ` crecientes (Clave de esto: `f(n)>=n`)
- Numerabilidad. Ocurre si 
	- Es el vacío `ø`
	- Existe una aplicación inyectiva de un conjunto a `ℕ`
- Un conjunto numerable:
	- `O` es finito 
	- `O` es equipotente a `ℕ` 
- Principio de los intervalos encajados
- Sucesiones:
	- Aplicaciones definidas en `ℕ` 
**SEGUIR A PARTIR DE AQUÍ **



## Consejos generales útiles
- Si no tienes ni idea de cómo hacer algo, intenta probar el contrario. Llegarás a una contradicción
- Para poder probar que dos números positivos son iguales, es suficiente probar que sus cuadrados son iguales
- Para probar una desigualdad entre dos números positivos, es suficiente probar dicha desigualdad para sus cuadrados.
