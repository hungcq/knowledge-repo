## 3. Binding model and implementation
- Consequences of the lack of tight association with impl:
  - Irrelevant, misleading model
  - Incorrect software
- Analysis model:
  - Fails to understand the domain: crucial discoveries always emerge during the design/impl effort
  - Divide between analysis & design process causes lost of info & insight
- -> Need a single model that serves both purposes: analysis & design
- -> Include both domain concepts & technical considerations
- -> Need to:
  - Choose between possible models
  - Multiple iterations & refactoring: model `<->` design/code
  - Implementation language supports modeling paradigm (eg OOP)
- Discussion about suitability of OOP paradigm to model driven design, compared to other paradigms
- System model should map to end users' model
- -> Give users more access to the potential of the software & yield consistent, predictable behavior
- Implication for division of responsibility: modelers should be involved in impl
