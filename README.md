# desafio-metassembly

La idea principal para enfrentar el metaensamblaje de genomas es reconocer los solapamientos entre los genomas fuente y luego decidir si estos son correctos, en el sentido de que los fragmentos estén unidos de la misma manera que en la secuencia original.

Los conceptos de genoma y gen pueden ser revisados en el siguiente link: 

https://www.khanacademy.org/science/high-school-biology/hs-molecular-genetics/hs-rna-and-protein-synthesis/a/intro-to-gene-expression-central-dogma

El genoma corresponde al ADN presente en la célula de un organismo, mientras que el gen es la unidad funcional del ADN: es un fragmento de ADN que codifica para la síntesis de una proteína, necesaria para llevar a cabo una reacción química en la célula. En bacterias y arqueas, también como organismos procariotas (carentes de núcleo), el ADN está contenido (disuelto) en el citoplasma, el fluido intracelular. Al contrario, los organismos eucariontes que comprenden protistas, hongos, plantas y animales tiene el ADN encerrado en un núcleo membranoso dentro de la célula.

ATTCCCGTAGCAAATCGCTCTCTCGGATCTAGGCTTTATTTAGGCTTAGGCTTGCGCGGCGCGGCGATAATTATATATCGGCAAAATTTG

Obtener el genoma de una bacteria, por ejemplo, ha sido un camino arduo en las ultimas decadas, convergiendo actualmentes en técnicas de secuenciación y herramientas bioinfórmaticas sofisticadas. Sin embargo, no siempre es posible recuperar el genoma completo como una secuencia única, sino que se encuentra fragmentado. Esta fragmentación provoca que ciertos genes no sea predichos correctamente, por lo que se pierde información biológica valiosa del organismo

Algunas herramientas de metaensamblaje creadas recientemente son:
- quickmerge: https://academic.oup.com/nar/article/44/19/e147/2468393
- metaassembler: https://genomebiology.biomedcentral.com/articles/10.1186/s13059-015-0764-4

Sin embargo, ambas presentan problemas a la hora de discriminar lecturas quiméricas, dando algunos resultados érroneos. Esto es lo que se quiere mejorar.

Dentro de los pases que hay realizar al inicio está la identificación del solapamiento de las secuencias. Esta se hace generalmente con mummer, que es un alineador rápido de genomas.  
  
`#alineamiento de genomas, especificar length`  
`nucmer -l length -prefix out assembly_1.fasta assembly2.fasta`  
`#filtrado de replicados, especificar minalignpc`  
`delta-filter -i minalignpc -r -q out.delta > out.rq.delta`  
`#resumen de solapamientos`  
`show-coords -r -c -l out.rq.delta > out.coords`    
  
En el archivo estan guardados los datos de los solapamientos encontrados.

Datos de entrenamiento:  
Eucariontes:  
Bacterias:

