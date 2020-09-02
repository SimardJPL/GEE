Below is the JavaScript code representing the imports of the tutorial video. To transfer them to another script, copy and paste the code below into the editor and click "Convert" in the suggestion tooltip. Otherwise, reproduce the imports manually and upload new files. Copy/paste the following:

var basins = ee.FeatureCollection("users/echoparkrs/Guyana/region1_inclusive"),
    sentinel1 = ee.ImageCollection("COPERNICUS/S1_GRD"),
    RedMangroves = /* color: #d67066 */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.708666040455064, 7.605316757040193]),
            {
              "class_id": 7,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.704374506031236, 7.601403258906361]),
            {
              "class_id": 7,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69750805095311, 7.596809106884119]),
            {
              "class_id": 7,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.74621696666356, 7.620545029515167]),
            {
              "class_id": 7,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71506042674657, 7.609825743246412]),
            {
              "class_id": 7,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69121029968169, 7.591524384887554]),
            {
              "class_id": 7,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69824841613677, 7.592034854927705]),
            {
              "class_id": 7,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.703140765379935, 7.5962036708955525]),
            {
              "class_id": 7,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70829060668853, 7.601733670470092]),
            {
              "class_id": 7,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71052220458892, 7.597649985352419]),
            {
              "class_id": 7,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70700314636138, 7.593396105404438]),
            {
              "class_id": 7,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68734791870025, 7.589992971130381]),
            {
              "class_id": 7,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.691124468993216, 7.586930127254435]),
            {
              "class_id": 7,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69455769653228, 7.588546630907129]),
            {
              "class_id": 7,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69859173889068, 7.585739015412593]),
            {
              "class_id": 7,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69610264892486, 7.585568856308846]),
            {
              "class_id": 7,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69507268066314, 7.593225949330603]),
            {
              "class_id": 7,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6750741302481, 7.582335820552557]),
            {
              "class_id": 7,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.67378666992095, 7.581399937248254]),
            {
              "class_id": 7,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.66786435241607, 7.574508370278218]),
            {
              "class_id": 7,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.666147738646536, 7.572211156788218]),
            {
              "class_id": 7,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.658937960814505, 7.561916086738326]),
            {
              "class_id": 7,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.65662053222564, 7.559618806177935]),
            {
              "class_id": 7,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.64657834167388, 7.545069078908844]),
            {
              "class_id": 7,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71146714131646, 7.607706577483235]),
            {
              "class_id": 7,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.74700104634576, 7.610471512071673]),
            {
              "class_id": 7,
              "system:index": "25"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7459281627398, 7.623445197714913]),
            {
              "class_id": 7,
              "system:index": "26"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7459281627398, 7.596051118929788]),
            {
              "class_id": 7,
              "system:index": "27"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.74215161244683, 7.5916696056302255]),
            {
              "class_id": 7,
              "system:index": "28"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72703751032548, 7.617232126418404]),
            {
              "class_id": 7,
              "system:index": "29"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72712334101396, 7.611532177792675]),
            {
              "class_id": 7,
              "system:index": "30"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72429092829423, 7.611447103358504]),
            {
              "class_id": 7,
              "system:index": "31"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71107300226884, 7.592985552183383]),
            {
              "class_id": 7,
              "system:index": "32"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.706953129221965, 7.590092887005221]),
            {
              "class_id": 7,
              "system:index": "33"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.73253067438798, 7.617317199704254]),
            {
              "class_id": 7,
              "system:index": "34"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.73527725641923, 7.623272287724282]),
            {
              "class_id": 7,
              "system:index": "35"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70807649747075, 7.600552493721426]),
            {
              "class_id": 7,
              "system:index": "36"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70769998892074, 7.596298642514999]),
            {
              "class_id": 7,
              "system:index": "37"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.705253814299155, 7.596936722881628]),
            {
              "class_id": 7,
              "system:index": "38"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.752907151005736, 7.620972909718163]),
            {
              "class_id": 7,
              "system:index": "39"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.747671479008666, 7.622589285142318]),
            {
              "class_id": 7,
              "system:index": "40"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.747971886418334, 7.622078851457064]),
            {
              "class_id": 7,
              "system:index": "41"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71150655045108, 7.604978971597803]),
            {
              "class_id": 7,
              "system:index": "42"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.709832852025784, 7.604298365254296]),
            {
              "class_id": 7,
              "system:index": "43"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71318024887637, 7.603490143819486]),
            {
              "class_id": 7,
              "system:index": "44"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.745884915744675, 7.62030858733762]),
            {
              "class_id": 7,
              "system:index": "45"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71447088376225, 7.610440042422754]),
            {
              "class_id": 7,
              "system:index": "46"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70462181225957, 7.6037616310037635]),
            {
              "class_id": 7,
              "system:index": "47"
            })]),
    Water = 
    /* color: #0b4a8b */
    /* locked: true */
    ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.749317675780325, 7.614835231222426]),
            {
              "class_id": 2,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7494035064688, 7.619684408682951]),
            {
              "class_id": 2,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75223591918853, 7.6249588902482435]),
            {
              "class_id": 2,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75841572875884, 7.6264901791747635]),
            {
              "class_id": 2,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76090481872466, 7.628531889219085]),
            {
              "class_id": 2,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76365140075591, 7.630828801371095]),
            {
              "class_id": 2,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75498250121978, 7.631339224618569]),
            {
              "class_id": 2,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71876195068267, 7.631339224618569]),
            {
              "class_id": 2,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70451405639556, 7.62700060759924]),
            {
              "class_id": 2,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70082333679107, 7.621300788970872]),
            {
              "class_id": 2,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70648816223052, 7.6177277296463215]),
            {
              "class_id": 2,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69172528381255, 7.617642656441969]),
            {
              "class_id": 2,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68485882873443, 7.61168749016742]),
            {
              "class_id": 2,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.66777852172759, 7.60547701437154]),
            {
              "class_id": 2,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.661684542845755, 7.595352895411156]),
            {
              "class_id": 2,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.65825131530669, 7.611091968989492]),
            {
              "class_id": 2,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68477299804595, 7.626830464858746]),
            {
              "class_id": 2,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.67584660644439, 7.6272558215831445]),
            {
              "class_id": 2,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.67378666992095, 7.61636655634974]),
            {
              "class_id": 2,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6915536224356, 7.632104858347445]),
            {
              "class_id": 2,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70168164367583, 7.6341465415883025]),
            {
              "class_id": 2,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.676704913329154, 7.611942713276184]),
            {
              "class_id": 2,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.665203601073294, 7.625469320499222]),
            {
              "class_id": 2,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68709042663482, 7.625979750141416]),
            {
              "class_id": 2,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75120595092681, 7.638485086094]),
            {
              "class_id": 2,
              "system:index": "24"
            })]),
    Forest = /* color: #308d00 */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.85833230601572, 7.535935172582695]),
            {
              "class_id": 3,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.832926422226656, 7.53661588686237]),
            {
              "class_id": 3,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81988015757822, 7.5549947676524205]),
            {
              "class_id": 3,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.79928079234384, 7.546486123631072]),
            {
              "class_id": 3,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.78863778697275, 7.5590788572687515]),
            {
              "class_id": 3,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77559152232431, 7.573032538521676]),
            {
              "class_id": 3,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.79619088755869, 7.587666401763438]),
            {
              "class_id": 3,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81850686656259, 7.601959461974724]),
            {
              "class_id": 3,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.835673004257906, 7.600598238633045]),
            {
              "class_id": 3,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.839449554550875, 7.580179371083057]),
            {
              "class_id": 3,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.85146585093759, 7.56894858097999]),
            {
              "class_id": 3,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.861422210800875, 7.559419196326627]),
            {
              "class_id": 3,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.84597268687509, 7.54342297079471]),
            {
              "class_id": 3,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.880648285019625, 7.5437633221809355]),
            {
              "class_id": 3,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81298352980741, 7.496792305080437]),
            {
              "class_id": 3,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81023694777616, 7.483006369382569]),
            {
              "class_id": 3,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.83220960402616, 7.480963971463339]),
            {
              "class_id": 3,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75135709548124, 7.503089439165537]),
            {
              "class_id": 3,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.847315805198036, 7.454922560846256]),
            {
              "class_id": 3,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.86568357253202, 7.4407948727392865]),
            {
              "class_id": 3,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.88319303298124, 7.45730549947918]),
            {
              "class_id": 3,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.820734276604085, 7.5945138650934]),
            {
              "class_id": 3,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81532694323006, 7.602000646146839]),
            {
              "class_id": 3,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.80270983202401, 7.598597580027933]),
            {
              "class_id": 3,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.812237038444906, 7.599533425899129]),
            {
              "class_id": 3,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.80335356218758, 7.596598266108098]),
            {
              "class_id": 3,
              "system:index": "25"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81644274218026, 7.609827595826719]),
            {
              "class_id": 3,
              "system:index": "26"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.811507477592855, 7.606935044099856]),
            {
              "class_id": 3,
              "system:index": "27"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.833045979892624, 7.54873772360846]),
            {
              "class_id": 3,
              "system:index": "28"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.83510591641606, 7.547035983570321]),
            {
              "class_id": 3,
              "system:index": "29"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.83467676297368, 7.554949017896793]),
            {
              "class_id": 3,
              "system:index": "30"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76506807461919, 7.570264156327316]),
            {
              "class_id": 3,
              "system:index": "31"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81888391629399, 7.615100346187117]),
            {
              "class_id": 3,
              "system:index": "32"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.828067799960984, 7.556565641492517]),
            {
              "class_id": 3,
              "system:index": "33"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.82789613858403, 7.555204274656245]),
            {
              "class_id": 3,
              "system:index": "34"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.78618242398442, 7.609315294356925]),
            {
              "class_id": 3,
              "system:index": "35"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.79596712247075, 7.609910818002263]),
            {
              "class_id": 3,
              "system:index": "36"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76406514050769, 7.593621212020511]),
            {
              "class_id": 3,
              "system:index": "37"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.78260456921863, 7.593876445871256]),
            {
              "class_id": 3,
              "system:index": "38"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7867244422655, 7.593025665779316]),
            {
              "class_id": 3,
              "system:index": "39"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81427609326648, 7.588006028963952]),
            {
              "class_id": 3,
              "system:index": "40"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.78500782849597, 7.577796417441809]),
            {
              "class_id": 3,
              "system:index": "41"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.780887955449096, 7.577966579618023]),
            {
              "class_id": 3,
              "system:index": "42"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77805554272937, 7.577456092887671]),
            {
              "class_id": 3,
              "system:index": "43"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77161824109363, 7.580433923617285]),
            {
              "class_id": 3,
              "system:index": "44"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.767342587863816, 7.597319570646681]),
            {
              "class_id": 3,
              "system:index": "45"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.784337064182175, 7.591789514250871]),
            {
              "class_id": 3,
              "system:index": "46"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.784337064182175, 7.591789514250871]),
            {
              "class_id": 3,
              "system:index": "47"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.765840550815476, 7.6057846729068554]),
            {
              "class_id": 3,
              "system:index": "48"
            })]),
    Agriculture = 
    /* color: #ddea12 */
    /* locked: true */
    ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.72627731798509, 7.586475291960281]),
            {
              "class_id": 4,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72601982591966, 7.584773700806349]),
            {
              "class_id": 4,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.724045720084696, 7.581795900095968]),
            {
              "class_id": 4,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72327324388841, 7.580264451708749]),
            {
              "class_id": 4,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72138496874192, 7.576435806910665]),
            {
              "class_id": 4,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71941086290696, 7.572096635002544]),
            {
              "class_id": 4,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.716320958121806, 7.569629243256974]),
            {
              "class_id": 4,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.730826344474345, 7.573543030493632]),
            {
              "class_id": 4,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.683084810340716, 7.524533049426852]),
            {
              "class_id": 4,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.65278657730849, 7.532531585137952]),
            {
              "class_id": 4,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.67990907486708, 7.573372866570175]),
            {
              "class_id": 4,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68179735001357, 7.575074502780913]),
            {
              "class_id": 4,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.685831392371966, 7.564949668406685]),
            {
              "class_id": 4,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69106706436904, 7.5606954654041045]),
            {
              "class_id": 4,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70445665177138, 7.546230861723205]),
            {
              "class_id": 4,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.706087434852435, 7.547932604929699]),
            {
              "class_id": 4,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.742565477454974, 7.614805794578373]),
            {
              "class_id": 4,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.74041971024306, 7.604681895708861]),
            {
              "class_id": 4,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.75415262039931, 7.6067237096759355]),
            {
              "class_id": 4,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.73235162552626, 7.59847131852275]),
            {
              "class_id": 4,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.67853578385146, 7.555760537397171]),
            {
              "class_id": 4,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.66943773087294, 7.561631393662775]),
            {
              "class_id": 4,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.66119798477919, 7.548358039684948]),
            {
              "class_id": 4,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.66892274674208, 7.534063202797279]),
            {
              "class_id": 4,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6699527150038, 7.535935172582695]),
            {
              "class_id": 4,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6754458790663, 7.525086144410794]),
            {
              "class_id": 4,
              "system:index": "25"
            })]),
    Wetlands = 
    /* color: #bf04c2 */
    /* locked: true */
    ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.78671933913358, 7.527170880702863]),
            {
              "class_id": 5,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7892084290994, 7.52572433005433]),
            {
              "class_id": 5,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.793156640769325, 7.525554147307878]),
            {
              "class_id": 5,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.79701902175077, 7.521554833545652]),
            {
              "class_id": 5,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.799164788962685, 7.522065386291445]),
            {
              "class_id": 5,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.78405858779081, 7.531680684098908]),
            {
              "class_id": 5,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77324392104276, 7.529978877008697]),
            {
              "class_id": 5,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7738447358621, 7.532616675149945]),
            {
              "class_id": 5,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77702047133573, 7.527681426838485]),
            {
              "class_id": 5,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77298642897733, 7.527426153845824]),
            {
              "class_id": 5,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.771956460715614, 7.530659600646658]),
            {
              "class_id": 5,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.776934640647255, 7.509301387531594]),
            {
              "class_id": 5,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77564718032011, 7.517980947507995]),
            {
              "class_id": 5,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.83581449294218, 7.5169598318072355]),
            {
              "class_id": 5,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.84147931838163, 7.5184064116745075]),
            {
              "class_id": 5,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.84577085280546, 7.51806604037465]),
            {
              "class_id": 5,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.84791662001737, 7.519597709122375]),
            {
              "class_id": 5,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.843110101462685, 7.50964176569911]),
            {
              "class_id": 5,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.84027768874296, 7.515087780119331]),
            {
              "class_id": 5,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.82697393202909, 7.51806604037465]),
            {
              "class_id": 5,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.81281186843046, 7.5190020608071055]),
            {
              "class_id": 5,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76613506024554, 7.550910639425099]),
            {
              "class_id": 5,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.76742252057269, 7.5499746879370955]),
            {
              "class_id": 5,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.77137073224261, 7.544188761037218]),
            {
              "class_id": 5,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7640751237221, 7.554824596413675]),
            {
              "class_id": 5,
              "system:index": "24"
            })]),
    MudFlat = /* color: #a78443 */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.74021962280181, 7.638570155153784]),
            {
              "class_id": 6,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.738331347655325, 7.635933006424882]),
            {
              "class_id": 6,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.734383135985404, 7.633551051650254]),
            {
              "class_id": 6,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.730091601561575, 7.631254154119635]),
            {
              "class_id": 6,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.726572543334036, 7.628361747087541]),
            {
              "class_id": 6,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.722881823729544, 7.625214105449831]),
            {
              "class_id": 6,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71996358032134, 7.622406729862881]),
            {
              "class_id": 6,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71695950622466, 7.619769481481782]),
            {
              "class_id": 6,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71455624694732, 7.6184933877251035]),
            {
              "class_id": 6,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.74365285034087, 7.640781944761751]),
            {
              "class_id": 6,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.746571093749075, 7.643248927349953]),
            {
              "class_id": 6,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.7479443847647, 7.643929471762526]),
            {
              "class_id": 6,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.73275235290435, 7.631339224618569]),
            {
              "class_id": 6,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.728117495726615, 7.62870203128296]),
            {
              "class_id": 6,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72502759094146, 7.625554392148536]),
            {
              "class_id": 6,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.64305928344634, 7.549238349070001]),
            {
              "class_id": 6,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.636965304564505, 7.543282236537002]),
            {
              "class_id": 6,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.63481953735259, 7.539793618259434]),
            {
              "class_id": 6,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.63130047912505, 7.53630497186663]),
            {
              "class_id": 6,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.627695590209036, 7.532901387327399]),
            {
              "class_id": 6,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.62237408752349, 7.528391596632176]),
            {
              "class_id": 6,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.618769198607474, 7.523201024746893]),
            {
              "class_id": 6,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.61370518798736, 7.519201689295204]),
            {
              "class_id": 6,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.59742898871256, 7.49673665274329]),
            {
              "class_id": 6,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.594510745304355, 7.494353929300527]),
            {
              "class_id": 6,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.59554071356607, 7.497587622241547]),
            {
              "class_id": 6,
              "system:index": "25"
            })]),
    BlackMangroves = /* color: #002100 */ee.FeatureCollection(
        [ee.Feature(
            ee.Geometry.Point([-58.676189929198294, 7.586845047946535]),
            {
              "class_id": 1,
              "system:index": "0"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6779923736563, 7.589992971130381]),
            {
              "class_id": 1,
              "system:index": "1"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.681683093260794, 7.594161806902984]),
            {
              "class_id": 1,
              "system:index": "2"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68374302978423, 7.594417040432657]),
            {
              "class_id": 1,
              "system:index": "3"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.684429675292044, 7.596288748351327]),
            {
              "class_id": 1,
              "system:index": "4"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.687691241454154, 7.598926141123185]),
            {
              "class_id": 1,
              "system:index": "5"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69069531555083, 7.600882905939869]),
            {
              "class_id": 1,
              "system:index": "6"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69533017272857, 7.603350118432571]),
            {
              "class_id": 1,
              "system:index": "7"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69824841613677, 7.60709344823466]),
            {
              "class_id": 1,
              "system:index": "8"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70219662780669, 7.607603899768269]),
            {
              "class_id": 1,
              "system:index": "9"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.705114871214896, 7.60939047535236]),
            {
              "class_id": 1,
              "system:index": "10"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69799092407134, 7.605306863084337]),
            {
              "class_id": 1,
              "system:index": "11"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69653180236724, 7.6081994257897865]),
            {
              "class_id": 1,
              "system:index": "12"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70408490295318, 7.6081994257897865]),
            {
              "class_id": 1,
              "system:index": "13"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70974972839263, 7.6122830105182]),
            {
              "class_id": 1,
              "system:index": "14"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71592953796294, 7.615515820843466]),
            {
              "class_id": 1,
              "system:index": "15"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72056439514068, 7.6167919234694645]),
            {
              "class_id": 1,
              "system:index": "16"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.724340945433646, 7.619003825683991]),
            {
              "class_id": 1,
              "system:index": "17"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72794583434966, 7.622661946586122]),
            {
              "class_id": 1,
              "system:index": "18"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.730349093627005, 7.6238529559494985]),
            {
              "class_id": 1,
              "system:index": "19"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.72691586608794, 7.620535135910776]),
            {
              "class_id": 1,
              "system:index": "20"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.722881823729544, 7.618408314672821]),
            {
              "class_id": 1,
              "system:index": "21"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.717903643797904, 7.615771041672701]),
            {
              "class_id": 1,
              "system:index": "22"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71326878662017, 7.612793455874727]),
            {
              "class_id": 1,
              "system:index": "23"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70871976013091, 7.610241223014816]),
            {
              "class_id": 1,
              "system:index": "24"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69160926431138, 7.603104784218446]),
            {
              "class_id": 1,
              "system:index": "25"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69344389527757, 7.604242675507376]),
            {
              "class_id": 1,
              "system:index": "26"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.68937766641099, 7.600552493721426]),
            {
              "class_id": 1,
              "system:index": "27"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.688058019575664, 7.599308246603058]),
            {
              "class_id": 1,
              "system:index": "28"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.697746158537456, 7.608921822923315]),
            {
              "class_id": 1,
              "system:index": "29"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69687712281663, 7.6057102317803835]),
            {
              "class_id": 1,
              "system:index": "30"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70381867974717, 7.610612684093994]),
            {
              "class_id": 1,
              "system:index": "31"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70618504776553, 7.6100409474012665]),
            {
              "class_id": 1,
              "system:index": "32"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70571297897891, 7.608381987121615]),
            {
              "class_id": 1,
              "system:index": "33"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.69700116409854, 7.605617039064483]),
            {
              "class_id": 1,
              "system:index": "34"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.6909071852167, 7.602511768467445]),
            {
              "class_id": 1,
              "system:index": "35"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.707926293765915, 7.611014295874533]),
            {
              "class_id": 1,
              "system:index": "36"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.70427848950566, 7.6074836884093004]),
            {
              "class_id": 1,
              "system:index": "37"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.709943314945114, 7.610993027241889]),
            {
              "class_id": 1,
              "system:index": "38"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71921302930058, 7.616203810700547]),
            {
              "class_id": 1,
              "system:index": "39"
            }),
        ee.Feature(
            ee.Geometry.Point([-58.71811868802251, 7.6157784429970015]),
            {
              "class_id": 1,
              "system:index": "40"
            })]),
    S2B03 = ee.Image("users/echoparkrs/Guyana/S2_B03"),
    S2B04 = ee.Image("users/echoparkrs/Guyana/S2_B04"),
    S2B05 = ee.Image("users/echoparkrs/Guyana/S2_B05");
