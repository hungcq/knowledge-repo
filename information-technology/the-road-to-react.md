# The Road to React

## Info
- Type: book
- Author: Robin Wieruch

## Category
- Software engineering
- Framework

## Style
- Hands-on
- Skim-able

## Takeaway
- Review of React imp concepts & principles
- React new features
- React optimization

## Main content
<img src="./resources/road-to-react.drawio.svg">

### Other notes
- Refresh behavior: bridge between React side & Dev server side:
  - React side: React fast refresh
  - Dev server side: Hot module replacement
- Key of item in list:
  - Help rerender more efficient: not update unchanged items
  - If there is no other choice, can use item's index
  - -> Can lead to bug when reordering items