## x-oca-geo object
The `x-oca-geo` object describes a specific location related to an event and its properties. 
It can be referenced to describe the geolocation information derived from techniques such as Geo IP, IP Location etc or user-supplied.

Please note that this object mimics the attributes of the [Location SDO](https://docs.oasis-open.org/cti/stix/v2.1/os/stix-v2.1-os.html#_th8nitr8jb4k)

| property name | type | description |
|--|--|--|
| type | `string` | x-oca-geo |
| extensions | `dictionary` | Specifies any extensions of the object, as a dictionary. |
| city_name | `string` | The city that this geolocation describes. |
| continent_name |`string`| Specifies the name of the continent.  |
| country_iso_code |`string`| Specifies the ISO code of the country.  |
| country_name |`string`| Specifies the name of the country.|
| location |`dictionary`| Specifies the longitude and latitude of the location. Each dictionary key SHOULD come from the location coordinates vocabulary. |
| name |`string`| Specifies a user-defined description of the location. This is not typically used in automated geolocation. |
| region_iso_code |`string`| Specifies the region ISO code. |
| region_name |`string`| Specifies the region name. |
| time_zone |`string`| Specifies the time zone of the geolocation such as an IANA time zone name |

### Location coordinates vocabulary
| value | type | description |
|--|--|--|
| lon | `double` | Specifies the longitude of the location. |
| lat | `double` | Specifies the latitude of the location. |

### Example

    {
	    "0":
	    {
	        "type": "x-oca-geo",
	        "name": "Dallas-1",
			"time_zone": "America/Chicago",
			"country_iso_code": "US",
			"country_name": "United States of America",
			"location":
				"lon": "-96.800496798",
				"lat": "32.785663524"
	    }
    }

