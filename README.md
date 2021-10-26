# hse21_hw1
Список команд
### создаем папку и делаем символические ссылки на файлы 
mkdir hw1  
cd hw1  
ln -s /usr/share/data-minor-bioinf/assembly/oil_R1.fastq  
ln -s /usr/share/data-minor-bioinf/assembly/oil_R2.fastq  
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R1_001.fastq  
ln -s /usr/share/data-minor-bioinf/assembly/oilMP_S4_L001_R2_001.fastq  
### параметр seed - 1205 выбираем случайно 5*10^5 чтений pair-end и 1,5*10^5 чтений mate pair  
seqtk sample -s1205 oil_R1.fastq 5000000 > sub_p_1.fastq  
seqtk sample -s1205 oil_R2.fastq 5000000 > sub_p_2.fastq  
seqtk sample -s1205 oilMP_S4_L001_R1_001.fastq 1500000 > sub_mp_1.fastq  
seqtk sample -s1205 oilMP_S4_L001_R2_001.fastq 1500000 > sub_mp_2.fastq  
### С помощью программы fastQC и multiQC оценить качество исходных чтений и получить по ним общую статистику  
### запускаем и вводим данные  
mkdir fastq  
fastqc sub_p_1.fastq  
fastqc sub_p_2.fastq  
fastqc sub_mp_1.fastq  
fastqc sub_mp_2.fastq  
mkdir multiqc  
multiqc -o multiqc fastqc  
### общая статистика исходных чтений

