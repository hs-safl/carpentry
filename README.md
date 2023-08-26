# Carpentry
Carpentry for useful MATLAB/Python code snippets


### Read a geotiff file and extract its longitude and latitude
#MATLAB #FileIO

File source: https://files.isric.org/soilgrids/latest/data_aggregated/5000m/soc/

Solution: https://www.mathworks.com/matlabcentral/answers/8865-geotiffread-getting-latlon-info#answer_12476

```matlab
dir_file = fullfile("Directory-to-file", "soc_0-5cm_mean_5000.tif");

% Read geotiff file
[A, R] = readgeoraster(dir_file);

% Read x, y from geoReference variable
[x, y] = worldGrid(R);

% Extract latitude and longitude from the projection
[lat, lon] = projinv(R.ProjectedCRS, x, y);

% Trim invalid latitude and longitude
[latlim,lonlim] = geoquadline(lat,lon);

% Plot figure
figure;
geoplot(latlim([1 2 2 1 1]),lonlim([1,1,2,2,1]),"r","LineWidth",2)
geobasemap("satellite")

mapshow(double(A), R)
```
