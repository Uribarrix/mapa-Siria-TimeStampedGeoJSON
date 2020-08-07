# mapa

mapa HTML da guerra Siria con TimeStampedGeoJSON

Este mapa HTML da guerra en Siria foi creado en catro pasos.

1- Creación dun contorno de Siria dende a unión dos polígonos que forman o nível administrativo 4 (provincial) de Siria. Descargados mediante a seguinte petición na API overpassTurbo:

'''html
<osm-script output="xml" timeout="25">
    <id-query {{geocodeArea:syria}} into="area_0"/>
    <union>
        <query type="node">
            <has-kv k="admin_level" v="4"/>
            <area-query from="area_0"/>
        </query>
        <query type="way">
            <has-kv k="admin_level" v="4"/>
            <area-query from="area_0"/>
        </query>
        <query type="relation">
            <has-kv k="admin_level" v="4"/>
            <area-query from="area_0"/>
        </query>
    </union>
    <union>
        <item/>
        <recurse type="down"/>
    </union>
    <print mode="meta"/><!-- fixed by auto repair -->
</osm-script>
'''

2- Atopouse múltiple documentación, superpoñer varios mapas e adicionar máis información non cartográfica, elaborouse un mapa cada 4 meses entre Xaneiro 2012 e Xaneiro 2018. Empregando QGIS 3.4 para xeorreferenciar os mapas dispoñíbles, dixitalizando os mesmos e dividindo o polígono de siria nos territorios dominados polos diferentes contendentes.

Unha vez rematada esta tarefa, exportáronse todos os mapas en formato geoJSON para o seu posterior tratamento en Python.

3- Buscáronse ducias de fotos públicas en internet de múltiples lugares de Siria, destruidos ou non, tratándose de lograr fotos e vídeos dos segundos tanto antes coma despois da sua destrucción. Ademáis creáronse as iconas e foron almacenadas nun servidor de imaxes. Con estes datos organizáronse os enlazamentos nunha folla de LibreOffice Calc, na que a partir dos enlazamentos, o nome do lugar as coordenadas, o tipo de recurso (foto/vídeo) e o estado de afectación pola guerra do lugar, con programación na propia folla é creado o código HTML que xera as xanelas emerxentes para cada caso. Todos os recursos están enlazados á fonte orixinal.

4- Con todo este material, constrúese o código para tratar as coordendas e implementar todos os datos que permiten a interpretación dos mesmos por TimeStampedGeoJSON. Este código busca directamente os arquivos .geojson e os .csv para, iterando por eles, contruir automáticamente todos os puntos e polígonos e representalos nas datas correspondentes.
