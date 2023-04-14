# Parcial_bioinformatica

### Punto 1

## Cambiar los nombres del FASTA
Se carga el archivo en atom y en find se coloca
(>\w+\.\d)\s(\w+)\s(\w+)\s\w+\s(\w+-\d)\s\w+\s\w+\s\w+\s\w+\s\((\w+)\)\s\w.+

Luego en replace se coloca
$1_$2_$3_$4_$5
y se da a reemplazar todo para luego subirlo 

## Subir archivo FASTA al cluster
scp -i bio.pt.pem -P 37022 /mnt/c/Users/barra/Downloads/Bioinformatica/sequence.fasta bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/parcial1_JuanDavidBarraza

## Descargar query desde el cluster
wget https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/query_parcial.fasta

## Hacer directorio y correr el BLAST
makeblastdb -in sequence.fasta -dbtype nucl -parse_seqids -out secuenciablast -title "Blast"

blastn -query query_parcial.fasta -task megablast -db secuenciablast -outfmt 7 -word_size 7 -out blast_secuencia -num_threads 1

## Resultado
La identidad mas probable del gen y la especie es de "Spodoptera_cilium_MA-6" es un gen mitocondrial que tiene el porcentaje de identidad mas alto y tiene poca probabilidad de ser al azar.

### Punto 2
Concatenar el popset y query
cat sequence.fasta query_parcial.fasta > Concatenado

## Alineamiento
Se carga clustalw2 con module load clustalw/2.1, luego se llama escribiendo clustalw2. A continuacion se selleciona la opción 1, se escribe Concatenar. Despues se selecciona la opcion 2, luego la 1 y se presiona enter hasta que te mande al menu principal y por ultimo se presiona x para salir del menu.

## Maxima verosimilitud
### Se carga FASconCAT para hacer la maxima verosimilitud
scp -i bio.pt.pem -P 37022 /mnt/c/Users/barra/Downloads/Bioinformatica/Clustal_ITS/FASconCAT-G_v1.05.1.pl bio.pt@172.25.255.10:/home/bio.pt/data/Parcial1/parcial1_JuanDavidBarraza y se abre escribiendo ./FASconCAT-G_v1.05.1.pl

![image](https://user-images.githubusercontent.com/130587993/232135485-3e52cffb-c0c5-4540-9bd4-84a88d9be430.png)

Se ven tres clados y todos son monofileticos. Entre mas larga rama mas diferente es la historia evolutiva respecto a su especie hermana. El primer grupo divergio primero que el segundo grupo en el primer clado. En el segundo grupo el segundo clado divirgio despues del tercer clado. Dentro del segundo y tercer clado la longitud de las ramas indican que las especies tienen historias evolutivas similares.

## Punto 3
## Descargar el archivo
wget https://raw.githubusercontent.com/paula-torres/bioinformatica_ur/main/files/archivo1.csv

## Mirar filas, columnas y caracteres
wc -l archivo 1.csv
wc -m archivo 1.csv

El archivo tiene 20 filas y tiene 908 caracteres

awk -F "\," '{print NF; exit}' archivo1.csv
El archivo tiene 4 columnas

### Cambiar chr por cromosoma, "," por tabulacion y renombrar
Se descarga el archivo y se cambia por atom. Se coloca "," en find y en replace se pone \t y luego se da a replace. Luego se sube al cluster

sed -i 's/chr/cromosoma/' archivo1.csv

mv archivo1.csv result_file.bed
grep -e "\scoding" result_file.bed > result_file_coding.bed

Aqui busca coding en result_file.bed y lo reemplaza en el result_file.bed






