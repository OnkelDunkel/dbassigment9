# DB assigment 9

## 1. Rewrite it as an expression in relational algebra

### Steps

Rename salesRepEmployeeNumber -> employeeNumber in customer table

<img src="https://latex.codecogs.com/gif.latex?A=\rho_{employeeNumber\,/\,salesRepEmployeeNumber}(customers)"/>

Natural join with employees

<img src="https://latex.codecogs.com/gif.latex?B=employees\bowtie\,A"/>

Project to remove unnecessary columns with names that are dublicate to those of offices

<img src="https://latex.codecogs.com/gif.latex?C=\Pi_{customerName,\,officeCode,\,city}(B)"/>

Natural join with offices. Since both D and the offices tables have city and office code the natural join will only join where both of these columns are a match.

<img src="https://latex.codecogs.com/gif.latex?D=offices\bowtie\,C"/>

Finally select only customerName and city

<img src="https://latex.codecogs.com/gif.latex?\Pi_{customerName,\,city}D"/>

### Final one-liner

<img src="https://latex.codecogs.com/gif.latex?\Pi_{customerName,\,city}offices\bowtie\Pi_{customerName,\,officeCode,\,city}\;(employees\bowtie\rho_{employeeNumber\,/\,salesRepEmployeeNumber}\;(customers))"/>

## 2. Add row counts to the subexpressions

<img src="https://latex.codecogs.com/gif.latex?\Pi_{customerName,\,city}(offices^{[7]}\bowtie(\Pi_{customerName,\,officeCode,\,city}\;(employees^{[23]}\bowtie(\rho_{employeeNumber\,/\,salesRepEmployeeNumber}\;(customers^{[122]})^{[122]})^{[100]})^{[100]})^{[14]})^{[14]}"/>

## 3. Rewrite to a better expression

### Steps

Natural join on employees and offices.

<img src="https://latex.codecogs.com/gif.latex?A=employees\bowtie\,offices"/>

Remove unwanted columns so only officeCode, city, employeeNumber are left.

<img src="https://latex.codecogs.com/gif.latex?B=\Pi_{officeCode,\,city,\,employeeNumber}\;A"/>

Natural join with customers after renaming employeeNumber -> salesRepEmployeeNumber.

<img src="https://latex.codecogs.com/gif.latex?C=customers\bowtie(\rho_{salesRepEmployeeNumber\,/\,mployeeNumber}\;B)"/>

Project only the columns that we want.

<img src="https://latex.codecogs.com/gif.latex?\Pi_{customerName,\,city}C"/>

### One liner

<img src="https://latex.codecogs.com/gif.latex?\Pi_{customerName,\,city}(customers\bowtie(\rho_{salesRepEmployeeNumber\,/\,mployeeNumber}\;(\Pi_{officeCode,\,city,\,employeeNumber}\;(employees\bowtie\,offices))))"/>

### With row numbers

<img src="https://latex.codecogs.com/gif.latex?(\Pi_{customerName,\,city}(customers^{[122]}\bowtie(\rho_{salesRepEmployeeNumber\,/\,mployeeNumber}\;(\Pi_{officeCode,\,city,\,employeeNumber}\;(employees^{[23]}\bowtie\,offices^{[7]})^{[23]})^{[23]})^{[23]})^{[14]})^{[14]}"/>