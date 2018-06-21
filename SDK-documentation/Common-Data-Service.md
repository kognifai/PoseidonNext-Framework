# Description
The common data service is used to fetch data from any time series data provider. You must register the data provider at first place in the common data service tagged with the realm name. 

## Data provider

Common data service supports various types of data provider and they can be registered as following: 

```typescript
interface ICommonDataService {
    /* Supported data provider */
    graphBrowse: IAssetRead;
    graphModification: IAssetWrite;
    timeSeries: ITimeSeriesRead;
    timeSeriesStreaming: ITimeSeriesStreaming;
    numericIndexedSeries: INumericIndexedSeriesRead;
    numericIndexedSeriesStreaming: INumericIndexedSeriesStreaming;

    /* Register data provider as */
    registerAssetReadProvider(graphProvider: IAssetRead, realm: string);
    registerAssetWriteProvider(graphProvider: IAssetWrite, realm: string);
    registerTimeSeriesProvider(timeSeriesProvider: ITimeSeriesRead, realm: string);
    registerTimeSeriesStreamingProvider(timeSeriesStreamingProvider: ITimeSeriesStreaming, realm: string);
    registerNumericIndexedSeriesProvider(numericIndexedSeriesProvider: INumericIndexedSeriesRead, realm: string);
    registerNumericIndexedSeriesStreamingProvider(numericIdexedStreamingProvider: INumericIndexedSeriesStreaming,realm: string);
    ....
```

- ```realm``` - the name of the Domain 


# Using the CommonDataService

### Example 
Let us say, we want to visualize real-time data from stock market and use it via application framework.
We first create stock data provider. In our case, one data provider to fetch the available stocks.

```typescript
export class StocksAsset implements IAssetRead {
// implementations
}
```
And one more data provider to get real-time data.
```typescript
export class StocksStreaming implements TimeSeriesStreaming {
// implementations
}
```

then we inject CommonDataService to our class/component and register our stock data provider.

## Injecting and Registering the provider 
The common data service can be used by injecting it into a class or a component, just like any standard Angular service and then the data providers are registered.
```typescript
@Injectable()
export class StockDataService{
  constructor(private commonDataService: CommonDataService) {
    commonDataService.registerAssetReadProvider(new StockAssetRead(), 'stock');
    commonDataService.registerTimeSeriesStreamingProvider(new StockTimeSeriesStreaming(), 'stock');
  }
   ...
}
```

Now, data providers are registered in CommonDataService, we can use these providers to get all available stocks as following:

```typescript
public getAllStocks(): Promise<StockDetails[]> {
    return new Promise<StockDetails[]>((resolve, reject) => {
      return this.commonDataService.graphBrowse.getRootVertices().then(root => {
        const stocks: StockDetails[] = root.vertices.map(v => stockId: v.vertexId, ...));
        resolve(stocks);
      }).catch((e) => reject(e));
    });
  }
```
and then start streaming on this stocks.
```typescript
public subscribe(stockId: string): Observable<StockPrice> {
    return Observable.create(observer => {
      const subscriber = this.commonDataService.timeSeriesStreaming.startDataStream(new StockAssetId(stockId), null).subscribe({
         next: x => {
            const stock = new StockPrice();
            stock.id = stockId;
            stock.price = x[0].value;
            observer.next(stock);
         },
         error: err => observer.error(err),
         complete: () => observer.complete(),
      });
    }
  }
```
