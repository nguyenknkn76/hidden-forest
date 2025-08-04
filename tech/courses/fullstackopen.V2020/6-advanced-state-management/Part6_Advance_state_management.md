# Flux architecture n Redux
- state and change state in App.js => to another comps because use props => app become bigger => hard to manage 
- Facebook dev Flux => tách state khỏi comps => save state vào stores riêng 
- change state of store => view be re renderer
    - action => dispatcher => store => view

# Redux 
- now facebook use Redux instead flux (redux have func like flux but it's simpler)
- state save in store 
- change state with action 

npm install redux
npm install react-redux