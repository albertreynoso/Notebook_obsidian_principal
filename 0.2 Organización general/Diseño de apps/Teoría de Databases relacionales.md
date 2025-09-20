Nomenclatura del model E-R
![[Pasted image 20250920151108.png|300]]
- Entidad: Cualquier tipo de objeto o concepto sobre el que se recoge información: cosa, persona, concepto abstracto o suceso. Por ejemplo: coches, casas, empleados, clientes, empresas, oficios, diseños de productos, conciertos, excursiones, etc.
	- Entidad fuerte: Es aquella que no depende de otra entidad para su existencia. Por ejemplo, la entidad PROVEEDOR es fuerte, pues no depende de otra para existir.
	- Entidad débil: Es aquella que necesita a otra entidad para existir. Por ejemplo, la entidad PRODUCTO necesita de la entidad PROVEEDOR
- Atributo: Dato (abstracción) para identificar o describir una entidad. Se representa con un nombre (del dato) dentro de una elipse unida o "conectada" por una línea a la entidad asociada. Cada entidad tendrá un valor por cada uno de los atributos, que posteriormente será almacenado en la base de datos. El valor de cada atributo está enmarcado en un conjunto de valores permitidos llamado Dominio.
	- Dominio: Es el conjunto de valores permitidos para el atributo.
- Clave Primaria: La clave primaria o principal (primary key - PK), son los atributos que identifican de forma única a cada entidad. No pueden contener valores nulos, no varia en el tiempo.
  ![[Pasted image 20250920151554.png|300]]
- Relación: Es una correspondencia o asociación entre dos o más entidades. Cada relación tiene un nombre que describe su función. Las relaciones se representan gráficamente mediante rombos y su nombre aparece en el interior. Tiene nombre de verbo que las identifica con respecto a las otras relaciones. Normalmente una relación no tiene atributos; si es que se diese el caso, se tendría q pensar en definir una nueva entidad.
  ![[Pasted image 20250920151727.png|300]]
	- Grado de relaciones: Es el número de conjuntos de entidades que participan en el conjunto de relaciones. Si en una relación participan dos entidades entonces la relación es de grado 2. Y así en forma sucesiva. En las relaciones en las que solo participa una entidad se llaman de grado 1 o anillo; una entidad se relaciona consigo misma.
	  ![[Pasted image 20250920151843.png|300]]
- Cardinalidad de relaciones: En el modelo E-R se representan ciertas restricciones a las que deben ajustarse los datos contenidos en una BD. Estas son las restricciones de las cardinalidades de asignación, que expresan el número de entidades a las que puede asociarse otra entidad mediante una relación.
	- Uno a uno:
	  ![[Pasted image 20250920152032.png|300]]
	- Uno a muchos: 
	  ![[Pasted image 20250920152055.png|300]]
	- Muchos a muchos:
	  ![[Pasted image 20250920152123.png|300]]
Ejemplo:
![[Pasted image 20250920152246.png]]
![[Pasted image 20250920152259.png]]

