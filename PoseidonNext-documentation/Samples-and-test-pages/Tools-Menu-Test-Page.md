# Sample usage

Below are the sample usage and definition of the tools menu service.

``` ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';

import { ToolsMenuTestComponent } from './toolsMenuTest.component';
import { ToolsMenuService } from '@kognifai/poseidon-ng-toolsmenuservice';

const routes: Routes = [
  { path: '', component: ToolsMenuTestComponent }
];

@NgModule({
  declarations: [
    ToolsMenuTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  exports: [ToolsMenuTestComponent],
  providers: [ToolsMenuService],
  bootstrap: []
})
export class ToolsMenuTestModule { }
```

And component looks like this

```ts
import { Component, OnInit, OnDestroy } from '@angular/core';
import { ToolsMenuService, ToolsMenuItem } from '@kognifai/poseidon-ng-toolsmenuservice';

@Component({
    selector: 'app-tools-menu-test-page',
    templateUrl: './toolsMenuTest.component.html',
    styleUrls: ['./toolsMenuTest.component.css']
})
export class ToolsMenuTestComponent implements OnInit, OnDestroy {
    cards = [];

    constructor(
        private toolsMenuService: ToolsMenuService,
    ) {
        this.cards = this.generateCards();
    }

    ngOnInit(): void {
        this.initToolsMenuItems();
    }

    private initToolsMenuItems() {
        const toggleFavoriteItem = new ToolsMenuItem();
        toggleFavoriteItem.label = 'Add Favorite';
        toggleFavoriteItem.icon = 'bookmark';
        toggleFavoriteItem.onSelected = () => this.toggleFavorite();
        const addCardItem = new ToolsMenuItem();
        addCardItem.label = 'Add Card';
        addCardItem.icon = 'plus';
        addCardItem.onSelected = () => this.addCard();
        const removeCardItem = new ToolsMenuItem();
        removeCardItem.label = 'Remove Card';
        removeCardItem.icon = 'minus';
        removeCardItem.onSelected = () => this.removeCard();
        const exportItem = new ToolsMenuItem();
        exportItem.label = 'Export';
        exportItem.icon = 'pull-up';
        const exportTimeSeriesItem = new ToolsMenuItem();
        exportTimeSeriesItem.label = 'Time Series';
        exportTimeSeriesItem.icon = 'angle-swap-horizontal';
        exportTimeSeriesItem.onSelected = () => this.exportTimeSeries();
        const exportDocumentItem = new ToolsMenuItem();
        exportDocumentItem.label = 'Document';
        exportDocumentItem.icon = 'attachment';
        const exportPdfItem = new ToolsMenuItem();
        exportPdfItem.label = 'PDF';
        exportPdfItem.icon = 'attachment';
        exportPdfItem.onSelected = () => this.exportPdf();
        const exportWordItem = new ToolsMenuItem();
        exportWordItem.label = 'Word';
        exportWordItem.icon = 'attachment';
        exportWordItem.onSelected = () => this.exportWord();
        const exportExcelItem = new ToolsMenuItem();
        exportExcelItem.label = 'Excel';
        exportExcelItem.icon = 'attachment';
        exportExcelItem.onSelected = () => this.exportExcel();
        exportDocumentItem.addChildren(exportPdfItem, exportWordItem, exportExcelItem);
        const printItem = new ToolsMenuItem();
        printItem.label = 'Print';
        printItem.icon = 'papers';
        printItem.onSelected = () => this.print();
        exportItem.addChildren(exportTimeSeriesItem, exportDocumentItem, printItem);
        this.toolsMenuService.register(toggleFavoriteItem, addCardItem, removeCardItem, exportItem);
    }

    ngOnDestroy(): void {
        this.toolsMenuService.clear();
    }

    private  toggleFavorite(): void {
        const toggleFavoriteItem: ToolsMenuItem = this.toolsMenuService.items[0];
        if (toggleFavoriteItem.label === 'Add Favorite') {
            toggleFavoriteItem.label = 'Remove Favorite';
            toggleFavoriteItem.icon = 'close';
        } else {
            toggleFavoriteItem.label = 'Add Favorite';
            toggleFavoriteItem.icon = 'bookmark';
        }
    }

    private  addCard(): void {
        this.cards.push(this.generateCards()[Math.floor(Math.random() * this.generateCards().length)]);
    }

    private  exportTimeSeries(): void {
        alert('Export Time Series clicked!');
    }

    private  exportPdf(): void {
        alert('Export PDF clicked!');
    }

    private  exportWord(): void {
        alert('Export Word clicked!');
    }

    private  exportExcel(): void {
        alert('Export Excel clicked!');
    }

    private  print(): void {
        alert('Print clicked!');
    }

    private  removeCard(): void {
        this.cards.splice(Math.floor(Math.random() * this.cards.length), 1);
    }

    private generateCards(): any[] {
        const result = [];
        result.push({
            title: 'Lorem Ipsum',
            text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis feugiat diam nec urna maximus fringilla.',
            icon: 'drilling-well'
        });
        result.push({
            title: 'Proin imperdiet',
            text: 'Maecenas pellentesque, velit non hendrerit varius, sapien velit rutrum risus, in pharetra felis nisl ac ipsum.',
            icon: 'renewables'
        });
        result.push({
            title: 'Lorem gravida',
            text: 'Maecenas vitae lorem rhoncus, pulvinar augue quis, sollicitudin justo, porta ut orci.',
            icon: 'cog'
        });
        result.push({
            title: 'Scelerisque',
            text: 'Proin dapibus libero et justo consequat aliquam. Nullam arcu tellus, elementum ac tempus vel, scelerisque a risus.',
            icon: 'subsea'
        });
        result.push({
            title: 'Donec ut mauris',
            text: 'Curabitur eu viverra lorem. Lorem ipsum dolor sit amet, consectetur adipiscing elit.',
            icon: 'info'
        });
        result.push({
            title: 'Integer id',
            text: 'Donec sit amet elementum mi. Etiam ac dolor ac orci tincidunt tristique eget facilisis velit.',
            icon: 'oil-gas-production'
        });
        result.push({
            title: 'Vestibulum',
            text: 'Praesent ultrices nunc aliquam, sollicitudin quam id, suscipit erat. Fusce sit amet metus leo.',
            icon: 'fishery'
        });
        return result;
    }

    closeInfoPanel() {
        document.getElementById('infoPanel').classList.add('kx-is-hidden');
    }
}

```

