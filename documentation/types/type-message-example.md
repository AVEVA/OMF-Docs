---
uid: typeExample
---

# Type Example


In the following example we create 2 `static` types and a `dynamic` type. The Type definitions define properties for the `isindex` and `isname` qualifiers. 
Their values will be referenced later when defining instance data and creating relationships.

### Headers

    omfversion = 1.2
    messagetype = type
    action = create
    messageformat = json

### Body

    [{
        "id": "Plant",
        "version": "1.0.0.0",
        "type": "object",
        "classification": "static",
        "properties": {
            "PlantId": {
                "type": "string",
                "isindex": true
            },
            "PlantName": {
                "type": "string",
                "isname": true
            },
            "Address": {
                "type": "string"
            },
            "Contact": {
                "type": "string"
            }
        }
    }, {
        "id": "Tank",
        "version": "1.0.0.0",
        "type": "object",
        "classification": "static",     
        "properties": {
            "TankName": {
                "type": "string",
                "isindex": true,
                "isname": true              
            },
            "Serial": {
                "type": "string"
            },
            "Model": {
                "type": "string"
            }
        }
    }, {
        "id": "TankPressure",
        "version": "1.0.0.0",
        "type": "object",
        "classification": "dynamic",        
        "properties": { 
            "Timestamp": {                        
                "type": "string", 
                "format":"date-time",
                "isindex": true     
            },
            "Pressure": {
                "type": "number",
                "name": "Tank Pressure",
                "description": "Tank Pressure in Pa",
                "uom": "pascal",
                "interpolation": "Continuous",
                "extrapolation": "Forward",
                "maximum": 20,
                "minimum": 10
            }                    
        }
    }]

### Inheritance Example

Properties of a Type definition can reference a previously defined Type using the `basetypeid` keyword, inheriting `static` data from another
`static` Type. In this example we reference the previously defined Type \'Tank\'. The resulting 'RectangularTank' contains the properties TankName, 
Serial, Model, TankHeight, and Tank Width, similarly the 'CylindricalTank' contains the properties TankName, Serial, Model, and TankDiameter.

    [{
        "id":"RectangularTank",
        "type": "object",
        "classification": "static",
        "basetypeid": "Tank",
        "properties": {                     
            "TankHeight": {
                "type": "integer",
                "format":"int32",
                "uom":"ft"              
            },
            "TankWidth": {
                "type": "integer",
                "format":"int32",
                "uom":"ft"
            }           
        }
    }, {
        "id":"CylindricalTank",
        "type": "object",
        "classification": "static",
        "basetypeid": "Tank",
        "properties": {                             
            "TankDiameter": {
                "type": "number",
                "format":"float32"      
            }
        }
    }]

### Reference Example

Properties of a Type definition can reference a previously defined Type using the `reftypeid`.
In this example we include the \'LocationProperties\' in the 'TankV2' Type, but cannot create instance data of the 'LocationProperties' Type.

	[{  
		"id":"LocationProperties",
		"type":"object",
		"properties": { 
			"Latitude":{ "type":"number", "format":"float32" },
			"Longitude":{ "type":"number", "format":"float32" }
		}
	}, {
		"id":"TankV2",
		"type":"object",
		"classification":"static",
		"properties": { 
			"TankName": { "type": "string", "isname": true,  "isindex":true },
			"Serial": { "type": "string" },
			"Model": { "type": "string" },
			"Location": { "reftypeid":"LocationProperties" }	
		}
	}]

### Enum Example

Properties of a Type definition can reference a previously defined `enum` using the `reftypeid` keyword. 
In this example we define data quality on the 'TankPressureV2' object to be of type 'DeviceStatusEnum'.

	[{
		"id": "DeviceStatusEnum", 
		"enum": {
			"values": [
				{"name": "Device Connected", "value": 0, "quality": "good"},
				{"name": "Device Failure", "value": 1, "quality": "bad"},
				{"name": "Uncertain - Out Limits", "value": 3, "quality": "questionable"} ]
			}
	}, {
		"id": "TankPressureV2",
		"type": "object",
		"basetypeid": "TankPressure",
		"classification": "dynamic",        
		"properties": {
			"DeviceStatus": {
				"reftypeid": "DeviceStatusEnum",
				"isquality": true
			}
		}
	}]
