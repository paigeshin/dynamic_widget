# dynamic_widget

https://www.notion.so/paigedream/App-Intent-Configuration-with-code-61380425c76446419f665a37a4f4fba3

```swift
import AppIntents
import SwiftUI

struct IncreaseCountIntent: AppIntent {
    
    static var title: LocalizedStringResource = "Increase Count"
    
    func perform() async throws -> some IntentResult {
        if let store = UserDefaults(suiteName: "group.dynamic_widget.test") {
            let count = store.integer(forKey: "count")
            store.setValue(count + 1, forKey: "count")
            return .result()
        }
        return .result()
    }
    
}

struct SetCountIntent: AppIntent {

    static var title: LocalizedStringResource = "Set Count"
    
    @Parameter(title: "Value")
    var value: Int  
    
    init(value: Int) {
        self.value = value
    }
    
    init() {
        self.value = -1 
    }
    
    func perform() async throws -> some IntentResult {
        if let store = UserDefaults(suiteName: "group.dynamic_widget.test") {
            store.setValue(self.count, forKey: "count")
            return .result()
        }
        return .result()
    }
    
    
}

```

```swift
struct MyWidgetEntryView : View {
    var entry: Provider.Entry

    var body: some View {
        VStack {
            Text(self.entry.count, format: .number)
            Button("Increase", intent: IncreaseCountIntent())
            Button("Set to 42", intent: SetCountIntent(value: 42))
        }
        .buttonStyle(.borderedProminent)
        
    }
}
```
