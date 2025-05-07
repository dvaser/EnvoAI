# EnvoAI

<img src="https://github.com/user-attachments/assets/ab2917ef-03e0-40b4-a74e-0bfb3237709d" style="width:20%;"></img>
<img src="https://github.com/user-attachments/assets/029ee331-3666-4659-af6f-5fcab7433d6e" style="width:20%;"></img>
<img src="https://github.com/user-attachments/assets/c3a7df4d-c12b-41bf-b98c-f24640429ba9" style="width:20%;"></img>


### Project Objective
An artificial intelligence-supported sustainability project that analyzes the potential impacts of public/private sector projects on nature according to location, sector, scale and environmental parameters.

<img src="https://github.com/user-attachments/assets/d3486592-162e-4399-b6bb-7160d0dd8071" style="width:75%;"></img>

### App Summary
> TR
```
Projede yer verdiğimiz özellik değerleri ile yapılan bu çalışma, mevcut konum özelinde çevresel faktörlerimizi değerlendiriyor.

Mesela bir inşaat yapmak istiyoruz ve bir yapı oluşturmak için seçeceğimiz konum ne kadar elverişli? Bu sadece bir inşaat yapısı olmak zorunda değil. Mesela bir ulaşım ihtiyacı olan metro hattı da olabilir. Ya da sadece konumunuzdaki mevcut çevre değerlerinizi merak etmiş de olabilirsiniz.

Projeyi özellik değeri üzerinden anlatmak gerekirse 'fault_line_distance' ve poi_density ile ele alabiliriz. 'fault_line_distance' bizim için fay hattına olan uzaklığımızı ifade ediyor. Ve konumumuzun en yakın fay hattına uzaklığını dönüyor. 'poi_density' ise bize mevcut konumun çevresindeki yapıları sayan bir özellik değeri. Eczane, market, ofis gibi veriler ile bize bir gelişmişlik seviyesi sunuyor.

Bu ve bunun gibi özellikler ile bize konumumuzun uygunluğunu ve makine öğrenimi ile eğitilmiş bu özellik değerleri üzerinden bir score döndürüyor.

Ne kadar da sürdürülebilir bir proje.
```

> ENG
```
This study, conducted with the property values we include in the project, evaluates our environmental factors specific to the current location.

For example, we want to build a building and how favorable is the location we choose to create a structure? It doesn't have to be just a construction structure. For example, it could be a metro line, which is a transportation need. Or you may just be curious about the current environmental values in your location.

If we need to explain the project through the property value, we can handle it with 'fault_line_distance' and poi_density. 'fault_line_distance' is our distance to the fault line. And it returns the distance of our location to the nearest fault line. 'poi_density' is a feature value that counts the structures around the current location. It gives us a level of development with data such as pharmacies, markets, offices, etc.

With these and similar features, it returns us the suitability of our location and a score based on these feature values trained with machine learning.

What a sustainable project.

Translated with DeepL.com (free version)
```

### Project Library
```
pip install geopandas
pip install shapely
pip install rasterio
pip install osmnx
pip install geopy
pip install scikit-learn=1.1.3
pip install pyqt5
```

### Project Structure 
```
envoai/
├── data/
│ ├── fault_lines.shp
│ ├── protected_area.shp
│ ├── ... (other data API)
├── features/
│ ├── elevation.py
│ ├── poi_density.py
│ ├── fault_line_distance.py
│ ├── green_area.py
│ └── ... (other feature scripts)
├── main.py
```

### Project Source Data
```
https://resourcewatch.org/data/explore/dis016rw1-Active-Fault-Lines_1
https://viewer.esa-worldcover.org/worldcover
https://resourcewatch.org/data/explore/bio040-Protected-Area-Connectivity
```

### Feature Information
| Feature                       | Description                          | Kütüphaneler                       | Fonksiyon Parametreleri                | Çıktı Değeri                     | Değer Tipi |
| ----------------------------- | ------------------------------------ | ---------------------------------- | -------------------------------------- | -------------------------------- | ---------- |
| `fault_line_distance`         | Fay hattına olan uzaklık (metre)     | `geopandas`, `shapely`             | `point: list[lon, lat]`                | float (metre)                    | Sayısal    |
| `slope_degree`                | Arazinin eğimi (derece)              | `rasterio`, `numpy`                | `point: list[lon, lat]`                | float (derece)                   | Sayısal    |
| `elevation`                   | Rakım yüksekliği (metre)             | `elevation`, `SRTM`, `rasterio`    | `point: list[lon, lat]`                | float (metre)                    | Sayısal    |
| `soil_type`                   | Arazi tipi (tarım, çorak vb.)        | `geopandas`                        | `point: list[lon, lat]`                | string                           | Kategorik  |
| `land_use`                    | Arazi kullanımı (konut, tarım vs.)   | `geopandas`, `osmnx`               | `point: list[lon, lat]`, `radius: int` | string                           | Kategorik  |
| `green_area_coverage`         | Belirli yarıçapta yeşil alan yüzdesi | `geopandas`, `osmnx`               | `point: list[lon, lat]`, `radius: int` | float (%)                        | Sayısal    |
| `water_proximity`             | Su kaynağına uzaklık                 | `geopandas`, `osmnx`               | `point: list[lon, lat]`, `radius: int` | float (metre)                    | Sayısal    |
| `climate_zone`                | İklim sınıfı (Köppen-Geiger)         | `geopandas`, `rasterio`            | Yok                                    | string                           | Kategorik  |
| `seasonal_accessibility`      | Tüm yıl boyunca erişilebilirlik      | `geopandas`                        | Yok                                    | string / boolean                 | Kategorik  |
| `disaster_risk_index`         | Afet riski skoru (deprem, sel...)    | `geopandas`, `custom_risk_data`    | `point: list[lon, lat]`                | float (0-1 arası skor)           | Sayısal    |
| `biodiversity_index`          | Biyoçeşitlilik skoru                 | `geopandas`, `biodiversity_data`   | `point: list[lon, lat]`                | float                            | Sayısal    |
| `protected_area_proximity`    | Koruma alanına uzaklık               | `geopandas`, `shapely`             | `point: list[lon, lat]`                | float (metre)                    | Sayısal    |
| `air_quality_index`           | Hava kalitesi (PM2.5, PM10)          | `openaq`, `requests`, `geopandas`  | `point: list[lon, lat]`                | float (AQI skoru)                | Sayısal    |
| `noise_pollution_potential`   | Gürültü kaynağına yakınlık           | `geopandas`, `osmnx`               | `point: list[lon, lat]`, `radius: int` | float (metre)                    | Sayısal    |
| `groundwater_pollution_risk`  | Yeraltı suyu kirliliği riski         | `geopandas`, `environmental_data`  | Yok                                    | float / string (low/medium/high) | Kategorik  |
| `transport_accessibility`     | Ulaşım altyapısına yakınlık          | `osmnx`, `networkx`                | `point: list[lon, lat]`, `radius: int` | float (mesafe veya erişim skoru) | Sayısal    |
| `infrastructure_availability` | Altyapı varlığı                      | `geopandas`, `infrastructure_data` | `point: list[lon, lat]`, `radius: int` | boolean / string                 | Kategorik  |
| `zoning_compliance`           | İmar planına uyum                    | `geopandas`, `zoning_data`         | `point: list[lon, lat]`, `radius: int` | boolean                          | Kategorik  |
| `poi_density`                 | Market, okul vb. POI yoğunluğu       | `osmnx`, `geopandas`               | `point: list[lon, lat]`, `radius: int` | int / float                      | Sayısal    |
| `socioeconomic_score`         | Gelir düzeyi ve sosyal seviye        | `geopandas`, `socioeconomic_data`  | `point: list[lon, lat]`                | float (skor)                     | Sayısal    |


### UI Views

<img src="https://github.com/user-attachments/assets/3be7a8f2-254b-4a57-a4eb-4675f98d3dc9" style="width:60%;"></img>
<img src="https://github.com/user-attachments/assets/6198cd3c-d687-4c61-965a-ab59694456af" style="width:60%;"></img>
<img src="https://github.com/user-attachments/assets/8cc52d9a-5ac3-454e-8062-bf71d222a4eb" style="width:60%;"></img>
<img src="https://github.com/user-attachments/assets/ab8e8418-bcd0-4ba3-aca3-5613ddd9b105" style="width:60%;"></img>

