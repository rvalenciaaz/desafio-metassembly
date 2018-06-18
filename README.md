# desafio-metassembly

La idea principal para enfrentar el metaensamblaje de genomas es reconocer los solapamientos entre los genomas fuente y luego decidir si estos son correctos, en el sentido de que los fragmentos estén unidos de la misma manera que en la secuencia original.

Los conceptos de genoma y gen pueden ser revisados en el siguiente link: 

https://www.khanacademy.org/science/high-school-biology/hs-molecular-genetics/hs-rna-and-protein-synthesis/a/intro-to-gene-expression-central-dogma

El genoma corresponde al ADN presente en la célula de un organismo, mientras que el gen es la unidad funcional del ADN: es un fragmento de ADN que codifica para la síntesis de una proteína, necesaria para llevar a cabo una reacción química en la célula. En bacterias y arqueas, también como organismos procariotas (carentes de núcleo), el ADN está contenido (disuelto) en el citoplasma, el fluido intracelular. Al contrario, los organismos eucariontes que comprenden protistas, hongos, plantas y animales tiene el ADN encerrado en un núcleo membranoso dentro de la célula.
  
ADN <- cadenas de nucleótidos <- cuatro núcleotidos [A (adenina), T (timina), G (guanina), C (citosina)]

ATTCCCGTAGCAAATCGCTCTCTCGGATCTAGGCTTTATTTAGGCTTAGGCTTGCGCGGCGCGGCGATAATTATATATCGGCAAAATTTG

Obtener el genoma de una bacteria, por ejemplo, ha sido un camino arduo en las ultimas decadas, convergiendo actualmentes en técnicas de secuenciación y herramientas bioinfórmaticas sofisticadas. Sin embargo, no siempre es posible recuperar el genoma completo como una secuencia única, sino que se encuentra fragmentado. Esta fragmentación provoca que ciertos genes no sea predichos correctamente, por lo que se pierde información biológica valiosa del organismo. 

Mientras el genoma esté en un menor número de fragmentos, conocidos contigs, y sea similar a la secuencia real, mejor el resultado del ensamblaje. Puede ocurrir que luego del ensamblaje del genoma de una bacteria con un software se llegen a 7 contigs, mientras que con otra herramientos se obtengan 5 contigs, donde cada contig es una secuencia de largo variable. Ahí es donde entra en juego el metaensamblaje, identificar los solapamientos y unir los fragmentos de ambos ensamblajes para obtener ojalá el genoma en un solo contig y de calidad. Estos solapamientos son esperables ya que ambos ensamblajes se originan de la misma bacteria.

Algunas herramientas de metaensamblaje creadas recientemente son:
- quickmerge: https://academic.oup.com/nar/article/44/19/e147/2468393 (identifica secuencias semillas [seed] que usa como base para unir los fragmentos, por ejemplo, en base a una métrica de calidad de solapamiento)
- metaassembler: https://genomebiology.biomedcentral.com/articles/10.1186/s13059-015-0764-4

Sin embargo, ambas presentan problemas a la hora de discriminar lecturas quiméricas, dando algunos resultados érroneos. Esto es lo que se quiere mejorar.

Dentro de los pasos que hay realizar al inicio está la identificación del solapamiento de las secuencias. Esta se hace generalmente con mummer, que es un alineador rápido de genomas.  
  
`#alineamiento de genomas, especificar length`  
`nucmer -l length -prefix out assembly_1.fasta assembly2.fasta`  
`#filtrado de replicados, especificar minalignpc`  
`delta-filter -i minalignpc -r -q out.delta > out.rq.delta`  
`#resumen de solapamientos`  
`show-coords -r -c -l out.rq.delta > out.coords`    
  
En el archivo estan guardados los datos de los solapamientos encontrados.  
  
Una vez realizada la generación de los archivos de solapamiento, se debe utilizar la información proveniente de la propia secuencia y los solapalmientos, para escoger las uniones correctas y reconstruir correctas. Si se genera un modelo, se puede entrenar en base a un set de datos (que esta en generación) que contiene genoma completos (en 1 contig) que serían la meta y 2 ensamblajes generados con diferentes herramientas de ese genoma, que son los que se deben comparar y unir para ser similar a la meta. La comparación del resultado del modelo con la meta puede ser realizado usando que penalize tanto equivocaciones en la posición de los nucleotidos, como 

Datos de entrenamiento:  
Eucariontes:  
Bacterias:

