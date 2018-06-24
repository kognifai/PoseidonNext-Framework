# Description

Unit of Measurement (UOM) service  is used to convert units from one to another unit. This service is the single source of truth for any units and dimensions specific operations.

# Using the Unit Of Measurement Service

## Injecting

Unit Of Measurement service can be used by injecting it into a class or a component, just like any standard Angular service.

First, import the following two lines of code into the component where Unit Of Measurement Service is to be used.

```javascript
import { UOMService } from '../your relative path';
import { UnitConversionService, IUnitConversionService, IUnitSet, IUnit } from '@kognifai/poseidon-unitofmeasurementservice';
```

And then inject it into the constructor in the following manner:

```javascript
constructor(private uomService: UOMService) { }
```

## Get all available Units 
```javascript
units(): Promise<IUnit[]>
```

Example:
```javascript
this.uomService.units.then((units) => {
      this.unit = units;
});
```

## Get list of convertible units
```
getConvertibleUnits(unit: string): Promise<IUnit[]> 
```

Example:
```javascript
this.uomService.getConvertibleUnits(unit).then((units) => {
      this.convertibleUnits = units;
});
```
- ```unit``` - the name of the unit for which convertible units are to be found

## Is a unit convertible
```javascript
isConvertible(sourceUnit: IUnit, targetUnit: IUnit): boolean
```

Example:
```javascript
const sourceUnit = this.uomService.findUnit(sourceUnit);
const targetUnit= this.uomService.findUnit(targetUnit);
this.isConvertibleUnit = this.uomService.isConvertible(munit, funit);
console.log("Is the unit convertible ?  " +   this.isConvertibleUnit);
```



## Does the unit exists
```javascript
exists (symbol: string): boolean
```
Example:
```javascript
this.exists = this.uomService.exists(unitName);
```

## Convert one unit to other
```javascript
convert(value: number, sourceUnit: any | IUnit, targetUnit: any | IUnit): number
```

Example:
```javascript
const sourceUnit = this.uomService.findUnit('ft');
const destUnit = this.uomService.findUnit('m');
this.convertToMeter = this.uomService.convert(myValToMeter, sourceUnit, destUnit);
console.log("The value in meter is   " + this.convertToMeter  + "  meter" );
```
## Find details of a unit
```javascript
findUnit(symbol: string): IUnit
```

Example:
```javascript
/** Find unit for meter */
this.unitForMeter = this.uomService.findUnit('m');
```
- ```unit``` - the name of the unit for which details are  to be found

