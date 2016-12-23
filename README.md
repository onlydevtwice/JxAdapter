# JxAdapter
The Easiest RecyclerAdapter for Android Kotlin

## Installation

### Gradle

``` Groovy
repositories {
   maven { url "https://jitpack.io" }
}

dependencies {
    compile 'com.github.judrummer.jxadapter:jxadapter:0.1.0' 
    compile 'com.github.judrummer.jxadapter:jxadapter-rxjava:0.1.0' 
}
```

## How to use

### ViewData

``` Kotlin
data class InvoiceHeaderViewData(val invoiceNumber: String)

data class InvoiceItemViewData(val productName: String, val price: Double, val quantity: Int, val totalAmount: Double)

data class InvoiceFooterViewData(val total: Double)

data class InvoiceSpaceViewData(val none: String = "")

```

### Adapter

``` Kotlin
    val jxAdapter = JxAdapter(
            JxViewHolder<InvoiceHeaderViewData>(R.layout.item_invoice_header) { view, position, item ->
                view.apply {
                    tvItemInvoiceHeaderNumber.text = item.invoiceNumber
                }
            },
            JxViewHolder<InvoiceItemViewData>(R.layout.item_invoice_item) { view, position, item ->
                view.apply {
                    tvItemInvoiceItemProductName.text = item.productName
                    tvItemInvoiceItemQuantity.text = "x ${item.quantity}"
                    tvItemInvoiceItemPrice.text = "$ ${item.price.format(2)}"
                    tvItemInvoiceItemTotal.text = "$ ${item.totalAmount.format(2)}"
                }
            },
            JxViewHolder<InvoiceFooterViewData>(R.layout.item_invoice_footer) { view, position, item ->
                view.apply {
                    tvItemInvoiceFooterTotal.text = "$ ${item.total.format(2)}"

                }
            },
            JxViewHolder<InvoiceSpaceViewData>(R.layout.item_invoice_space) { view, position, item ->

            })

```

### Assign Adapter to RecyclerView
``` Kotlin
  rvExample.apply {
            layoutManager = LinearLayoutManager(this@SimpleActivity)
            adapter = jxAdapter
        }
  jxAdapter.items = listOf(....) // Your Data
```