# Sample usage

Below are the sample usage and definition of the unit of measurement service.

``` ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';
import { UomServiceTestComponent } from './uomserviceTest.component';
import { HttpClientModule } from '@angular/common/http';
import { UOMService } from '@kognifai/poseidon-ng-uomservice';

const routes: Routes = [
  { path: '', component: UomServiceTestComponent }
];

@NgModule({
  declarations: [
    UomServiceTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    HttpClientModule,
    RouterModule.forChild(routes)
  ],
  exports: [UomServiceTestComponent],
  providers: [UOMService]
})
export class UomServiceTestModule { }
```
And its component looks like this

``` ts
import { Component } from '@angular/core';
import { UOMService } from '@kognifai/poseidon-ng-uomservice';
import { IUnit } from '@kognifai/poseidon-unitofmeasurementservice';

@Component({
  selector: 'app-uom-service-test-page',
  templateUrl: './uomserviceTest.component.html'
})
export class UomServiceTestComponent {
  unitForFeet: string;
  funit: IUnit;
  convertFM: any;
  unitForMeter: string;
  munit: IUnit;
  convertArr1: number[];
  convertMF: any;
  isConvertibleUnit: boolean;
  exists: boolean;
  public unit: IUnit[];
  public convertibleUnits: IUnit[];

  constructor(private uomService: UOMService) {}

  loadUnits() {
    this.uomService.units.then(units => {
      this.unit = units;
    });
  }
  getConvertibleUnitsAll(unit: string) {
    this.uomService.getConvertibleUnits(unit).then(units => {
      this.convertibleUnits = units;
    });
  }
  convertArray(
    values: number[],
    sourceUnit: IUnit | string,
    targetUnit: IUnit | string
  ) {
    this.convertArr1 = this.uomService.convertArray(
      values,
      sourceUnit,
      targetUnit
    );
  }
  isConvertible(sourceUnit: any, targetUnit: any) {
    const munit = this.uomService.findUnit(sourceUnit);
    const funit = this.uomService.findUnit(targetUnit);
    this.isConvertibleUnit = this.uomService.isConvertible(munit, funit);
  }
  doesUnitExists(val) {
    this.exists = this.uomService.exists(val);
  }
  convertMeterToFeet(myValToMeter) {
    const sourceU = this.uomService.findUnit('m');
    const destU = this.uomService.findUnit('ft');
    this.convertMF =
      this.uomService.convert(myValToMeter, sourceU, destU).toFixed(3) + '  ft';
  }

  convertFeetToMeter(myValToMeter) {
    const sourceU = this.uomService.findUnit('ft');
    const destU = this.uomService.findUnit('m');
    this.convertFM =
      this.uomService.convert(myValToMeter, sourceU, destU).toFixed(3) + '   m';
  }
  findUnitForMeter() {
    this.unitForMeter = JSON.stringify(this.uomService.findUnit('m'));
  }
  findUnitForFeet() {
    this.unitForFeet = JSON.stringify(this.uomService.findUnit('ft'));
  }
}
```


