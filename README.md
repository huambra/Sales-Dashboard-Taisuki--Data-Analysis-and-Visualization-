# Taisuki-Sales-Dashboard
### Data Analysis and Visualization
&nbsp;<br>
&nbsp;<br>

![Alt text](../../../../../../../../C:/Users/luisr/Documents/My%20life/Personal%20Brand/Projects/Sales%20Dashboard%20Taisuki%20(Data%20Analysis%20and%20Visualization)/taisuki-logo.png)

## Table of Contents

- [Taisuki-Sales-Dashboard](#taisuki-sales-dashboard)
    - [Data Analysis and Visualization](#data-analysis-and-visualization)
  - [Table of Contents](#table-of-contents)
  - [Project Description](#project-description)
  - [Action](#action)
  - [Results](#results)

## Project Description
Dashboards are an interactive way to view at a glance how a project or company is performing. In the restaurant -Taisuki Taiyaki- they had the problem that, although they were storing data, they did not have a functional dashboard for decision making. I was in charge of developing a sales dashboard in order to understand the restaurant's peak hours, so that they can reschedule the opening hours.

## Action
My role in the project was accessing the data, then transforming it and analyzing it in order to develop a dashboard, to finally present the information to the shareholders in order to facilitate the decision making regarding working hours. 

The first thing I did was to understand the project requirements and from where I should access the data to help me develop the dashboard.

Next I determined a few key metrics such as total sales per month, day, and product, number of orders, average ticket, etc. In order to give me a framework on how the sales were happening and during what times. 
 
Once I was clear about that, I started accessing the data using SQL and then applying transformations in Power BI. 

``` sql
/***QUERY RESUMEN***/
select 
--convert(varchar(10),b.FHATT,103) Fecha, 
case when b.FHATT='1900/01/01' then c.FECEM else b.FHATT end FHATT,
a.IDORD,
b.IDCTA, 
sum(b.PRTOT) Subtotal,  
sum(b.PRTOT)*0.12 IVA

from SLSCAB a														/*JOIN CABECERA CON DETALLE*/
inner join SLSDET b
on a.CDAMB=b.CDAMB and a.IDORD=b.IDORD
left outer JOIN (select IDAMB,IDORD,IDCTA,FECEM from DOCVEN) c		/*JOIN PARA ARREGLAR PROBLEMA DE FECHAS EN SEPT 2021*/
on a.CDAMB=c.IDAMB and a.IDORD=c.IDORD and c.IDCTA=b.IDCTA
WHERE a.CDAMB='2' AND a.IDORD  in
(select a.IDORD from SLSCAB a										/*SE FILTRAN SOLO LAS ORDENES QUE SE HAYAN FACTURADO*/
inner join 
DOCVEN b
on a.CDAMB=b.IDAMB and a.IDORD=b.IDORD
) 
group by 
convert(varchar(10),b.FHATT,103),case when b.FHATT='1900/01/01' then c.FECEM else b.FHATT end , a.IDORD,b.IDCTA
--order by convert(int,a.IDORD)
order by FHATT
```
![Alt text](../../../../../../../../C:/Users/luisr/Documents/My%20life/Personal%20Brand/Projects/Sales%20Dashboard%20Taisuki%20(Data%20Analysis%20and%20Visualization)/BI%20Measures.jpg)
&nbsp;<br>

After I had the raw data, I started designing and creating the final dashboard. 
1. first version
![Alt text](../../../../../../../../C:/Users/luisr/Documents/My%20life/Personal%20Brand/Projects/Sales%20Dashboard%20Taisuki%20(Data%20Analysis%20and%20Visualization)/first_version_page1.jpg)
![Alt text](../../../../../../../../C:/Users/luisr/Documents/My%20life/Personal%20Brand/Projects/Sales%20Dashboard%20Taisuki%20(Data%20Analysis%20and%20Visualization)/first_version_page2.jpg)
![Alt text](../../../../../../../../C:/Users/luisr/Documents/My%20life/Personal%20Brand/Projects/Sales%20Dashboard%20Taisuki%20(Data%20Analysis%20and%20Visualization)/first_version_page3.jpg)

2. final version

Finally, I presentented the dashboard to the shareholder and it was decided to cut 2 hours from Tuesdays and Fridays where I found that the restaurant was not even selling to the point of break even.

## Results
Developing and using a dashboard in the decision to reschedule the opening hours resulted in resource optimization saving 16% in personel.