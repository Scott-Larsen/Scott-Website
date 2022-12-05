---
layout: post
title: List of Time Zones With Largest City and Positive Negative in LibreOffice Calc
---

I was surprised that I wasn't able to quickly find a list of timezones showing the UTC offset along with the biggest city (or cities) to populate a dropdown that I'm adding to a website. This is far from perfect but I manually typed one out based on a [really great map that someone had posted to Reddit](https://www.reddit.com/r/MapPorn/comments/a676cb/most_populous_cities_per_timezone_dec_2018/)

<table>
<tr>
<th>Text</th>
<th>CSV</th>
</tr>
<tr>
<td>

```
Offset	City
-11	Pago Pago
-10	Honolulu
-09	Anchorage
-08	Los Angeles
-07	Phoenix
-06	Mexico City
-05	New York
-04	Manaus
-03	Santiago
-02	Sao Paulo
-01	Praia
+00	London
+01	Lagos
+02	Cairo
+03	Moscow
+04	Baku
+05	Karachi
+06	Dhaka
+07	Jakarta
+08	Shanghai
+09	Tokyo
+10	Brisbane
+11	Sydney
+12	Auckland
```

</td>
<td>

```
Offset,City
-11,Pago Pago
-10,Honolulu
-09,Anchorage
-08,Los Angeles
-07,Phoenix
-06,Mexico City
-05,New York
-04,Manaus
-03,Santiago
-02,Sao Paulo
-01,Praia
+00,London
+01,Lagos
+02,Cairo
+03,Moscow
+04,Baku
+05,Karachi
+06,Dhaka
+07,Jakarta
+08,Shanghai
+09,Tokyo
+10,Brisbane
+11,Sydney
+12,Auckland
```

</td>
</tr>
</table>

And in writing it out in LibreOffice I also stumbled over how to have the +01 GMT offset format still read as an integer while adding the sign and maintaining two digit places. This retains the + (addition / plus sign) before positive values and the negative before negative values (much more common). That was solved with a Google search by adding the following formatting to the respective cells (*Select cells*, Format => Cells > `Format Code` [bottom left corner]).

```
"+"00;"-"00
```
If you wanted nothing before 00 you could add a third component like the following.

```
"+"00;"-"00;""00
```