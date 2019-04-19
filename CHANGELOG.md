# Change Log

* **v1.3.0** (2019-04-19)
    * **Compatible with Pilosa 1.2 and 1.3**
    * Deprecated `QueryResponse.Columns` function. Use `QueryResponse.ColumnAttrs` function instead.
    * Deprecated `QueryResponse.Column` function.
    * Removed support for Go 1.9.
    * Added `Rows` and `GroupBy` calls.
    * Added `index.Opts` and `field.Opts` functions, which return the options for an `Index` or `Field`.
    * Added roaring import support for `RowKeyColumnID`, `RowIDColumnKey` and `RowKeyColumnKey` type data. Pass `OptImportRoaring(true)` to `client.ImportField` to activate that.
    * Added `OptClientManualServerAddress` function. Passing this option together with a single `URI` or address to `NewClient` causes the client use only the provided server address for fragment node and coordinator node addresses.
    * Added support for [Open Tracing](https://opentracing.io). See: [Tracing documentation](docs/tracing.md).
    * Added `OptImportSort` which enables/disables bit sorting before imports. Disabling bit sorting may improve import performance for already sortedd data.
    * Added support for automatically loading shard width per index.
    * Field option getters are attached to `Field` type instead of `*Field` type.
    * Performance improvements.
    * Deprecated `field.Options`. Use `field.Opts` instead.
    * Deprecated `Range` call. Use `RowRange` instead.

* **v1.2.0** (2018-12-21)
    * **Compatible with Pilosa 1.2**
    * Added support for roaring imports which can speed up the import process by %30 for non-key column imports.
    * Added mutex and bool fields.
    * Added `field.ClearRow` call.
    * Added `index.Options` call.
    * Added support for roaring importing `RowIDColumnID` with timestamp data.
    * Added support for clear imports. Pass `OptImportClear(true)` to `client.ImportField` to use it.
    * Added experimental *no standard view* support for time fields. Use `OptFieldTypeTime(quantum, true)` to activate it. See https://github.com/pilosa/pilosa/issues/1710 for more information.
    * Added `keys` and `trackExistence` to index options.
    * Removed experimental import strategies.

* **v1.1.0** (2018-09-25)
    * Compatible with Pilosa 1.1.
    * Added support for `Not` queries. See [Not call](https://www.pilosa.com/docs/master/query-language/#not). Usage sample: `index.Not(field.Row(1))`. This feature requires Pilosa on master branch.

* **v0.10.0** (2018-09-05)
    * Compatible with Pilosa 1.0.
    * Following terminology was changed:
        * frame to field
        * bitmap to row
        * bit to column
        * slice to shard
    * There are three types of fields:
        * Set fields to store boolean values (default)
        * Integer fields to store an integer in the given range.
        * Time fields which can store timestamps.
    * Experimental: Import strategies are experimental and may be removed in later versions.
    * Moved CSV related functionality to the `csv` subpackge.
    * Renamed `FilterFieldTopN` function to `FilterAttrTopN`.
    * Removed all deprecated code.
    * Removed `Field` type and renamed `Frame` to `Field`.
    * Removed `client.ImportValueField` function. `client.ImportField` function imports both set and integer fields, depending on the type of the field.
    * Removed index and field validation. The validation is done only on the server side. `schema.Index` and `index.Field` functions do not return `error` values.

* **v0.9.0** (2018-05-10)
    * Compatible with Pilosa 0.9.
    * Added `Equals`, `NotEquals` and `NotNull` field operations.
    * Added `Field.Min` and `Field.Max` functions.
    * It is possible to set the number of import goroutines and track the import progress. See: [Importing and Exporting Data](docs/imports-exports.md).
    * **Breaking Change** The signature of `Client.ImportFrame` function was changed. See: [Importing and Exporting Data](docs/imports-exports.md).
    * **Deprecation** `TimeQuantum` for `IndexOptions`. Use `TimeQuantum` of individual `FrameOptions` instead.
    * **Deprecation** `IndexOptions` struct is deprecated and will be removed in the future.
    * **Deprecation** Passing `IndexOptions` or `nil` to `schema.Index` function.
    * **Deprecation** `SocketTimeout` client option. Use `OptClientSocketTimeout` instead.
    * **Deprecation** `ConnectTimeout` client option. Use `OptClientConnectTimeout` instead.
    * **Deprecation** `PoolSizePerRoute` client option. Use `OptClientPoolSizePerRoute` instead.
    * **Deprecation** `TotalPoolSize` client option. Use `OptClientTotalPoolSize` instead.
    * **Deprecation** `TLSConfig` client option. Use `OptClientTLSConfig` instead.
    * **Deprecation** `ColumnAttrs` query option. Use `OptQueryColumnAttrs` instead.
    * **Deprecation** `Slices` query option. Use `OptQuerySlices` instead.
    * **Deprecation** `ExcludeAttrs` query option. Use `OptQueryExcludeAttrs` instead.
    * **Deprecation** `ExcludeBits` query option. Use `OptQueryExcludeBits` instead.
    * **Deprecation** `CacheSize` frame option. Use `OptFrameCacheSize` instead.
    * **Deprecation** `IntField` frame option. Use `OptFrameIntField` instead.
    * **Deprecation** `RangeEnabled` frame option. All frames have this option `true` on Pilosa 0.10.
    * **Deprecation** `InverseEnabled` frame option and `Frame.InverseBitmap`, `Frame.InverseTopN`, `Frame.InverseBitmapTopN`, `Frame.InverseFilterFieldTopN`, `Frame.InverseRange` functions. Inverse frames will be removed from Pilosa 0.10.
    * **Removed** `NewClientFromAddresses` function. Use `NewClient([]string{address1, address2, ...}, option1, option2, ...)` instead.
    * **Removed** `NewClientWithURI` function. Use `NewClient(uri)` instead.
    * **Removed** `NewClientWithCluster` function. Use `NewClient(cluster, option1, option2, ...)` instead.

* **v0.8.0** (2017-11-16)
    * IPv6 support.
    * **Deprecation** `Error*` constants. Use `Err*` constants instead.
    * **Deprecation** `NewClientWithURI`, `NewClientFromAddresses` and `NewClientWithCluster` functions. Use `NewClient` function which can be used with the same parameters.
    * **Deprecation** Passing a `*ClientOptions` struct to `NewClient` function. Pass 0 or more `ClientOption` structs to `NewClient` instead.
    * **Deprecation** Passing a `*QueryOptions` struct to `client.Query` function. Pass 0 or more `QueryOption` structs instead.
    * **Deprecation** Index options.
    * **Deprecation** Passing a `*FrameOptions` struct to `index.Frame` function. Pass 0 or more `FrameOption` structs instead.

* **v0.7.0** (2017-10-04):
    * Dropped support for Go 1.7.
    * Added support for creating range encoded frames.
    * Added `Xor` call.
    * Added support for excluding bits or attributes from bitmap calls. In order to exclude bits, pass `ExcludeBits: true` in your `QueryOptions`. In order to exclude attributes, pass `ExcludeAttrs: true`.
    * Added range field operations.
    * Customizable CSV timestamp format.
    * `HTTPS connections are supported.
    * **Deprecation** Row and column labels are deprecated, and will be removed in a future release of this library. Do not use `ColumnLabel` option for `IndexOptions` and `RowLabel` for `FrameOption` for new code. See: https://github.com/pilosa/pilosa/issues/752 for more info.

* **v0.5.0** (2017-08-03):
    * Supports imports and exports.
    * Introduced schemas. No need to re-define already existing indexes and frames.
    * `NewClientFromAddresses` convenience function added. Create a client for a
      cluster directly from a slice of strings.
    * Failover for connection errors.
    * *make* commands are supported on Windows.
    * **Deprecation** `NewIndex`. Use `schema.Index` instead.
    * **Deprecation** `CreateIndex`, `CreateFrame`, `EnsureIndex`, `EnsureFrame`. Use schemas and `client.SyncSchema` instead.

* **v0.4.0** (2017-06-09):
    * Supports Pilosa Server v0.4.0.
    * Updated the accepted values for index, frame names and labels to match with the Pilosa server.
    * `Union` query now accepts zero or more variadic arguments. `Intersect` and `Difference` queries now accept one or more variadic arguments.
    * Added `inverse TopN` and `inverse Range` calls.
    * Inverse enabled status of frames is not checked on the client side.

* **v0.3.1** (2017-05-01):
    * Initial version.
    * Supports Pilosa Server v0.3.1.
