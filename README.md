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
![image](https://user-images.githubusercontent.com/60805733/138952241-208549c6-83a4-451d-8894-9b3a635d97e6.png)
![image](https://user-images.githubusercontent.com/60805733/138952335-61e21339-337a-4f82-8e7e-cc936ae732d5.png)
![image](https://user-images.githubusercontent.com/60805733/138952365-6e3c2423-7877-4a3c-ac6a-ba4d09268709.png)
![image](https://user-images.githubusercontent.com/60805733/138952411-944832ca-dca3-49fa-93d9-9014591ae69e.png)
### С помощью программ platanus_trim и platanus_internal_trim подрезать чтения по качеству и удалить праймеры
platanus_trim sub_p_1.fastq sub_p_2.fastq  
platanus_internal_trim sub_mp_1.fastq sub_mp_2.fastq  
### удаляем исходники
rm sub_p_1.fastq  
rm sub_p_2.fastq  
rm sub_mp_1.fastq  
rm sub_mp_2.fastq 
### С помощью программы fastQC и multiQC оценить качество подрезанных чтений и получить по ним общую статистику
mkdir trimmed_fq
ls sub* | xargs -tI{} fastqc -o trimmed_fq {}
mkdir multiqc_trimmed
multiqc -o multiqc_trimmed trimmed_fq
### общая статистика обрезанных чтений
![image](https://user-images.githubusercontent.com/60805733/138956270-35829c17-d77e-4723-a6db-d6f3397f31ce.png)
![image](https://user-images.githubusercontent.com/60805733/138956306-2c147ded-3400-44a0-8617-c11a9ab4d788.png)
![image](https://user-images.githubusercontent.com/60805733/138956385-83e23f97-7a17-4e17-9819-1aa20af7abca.png)
![image](https://user-images.githubusercontent.com/60805733/138956423-263d3e9c-7cf4-447c-9a6c-2e7c0eeb7cfe.png)
![image](https://user-images.githubusercontent.com/60805733/138956466-12cf30d4-ee4d-48a7-b67e-9296f49a531c.png)
