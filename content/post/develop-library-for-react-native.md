+++
date = "2016-08-09T11:32:31+08:00"
title = "Developing react-native-image-viewer library for React Native"
url = "/developing-react-native-image-viewer-library.html"
+++

I was developing a [simple twitter client](https://itunes.apple.com/cn/app/zuo-ri-re-tui/id1137163693?l=en&mt=8 "昨日热推 app") with [React Native](https://github.com/facebook/react-native) recently. There will be many photos on user timeline, and I wanted to show them in fullscreen mode that users can swipe through. There were some libraries on npm site, but none of them fit well for my requirement, so I decided to develop one myself.

## Setup

Let's initialize the library project first:

{{< highlight bash >}}
$ npm init
{{< /highlight >}}

And then install `react` and `react-native` packages from npm as `peerDependencies`:

{{< highlight javascript >}}
"peerDependencies": {
    "react": "^15.2.1",
    "react-native": "^0.30.0"
}
{{< /highlight >}}

Since the [`symlink` support won't land](https://github.com/facebook/react-native/pull/9176) until React Native 0.32.0 release, so I use `npm install /path/to/local/package_name` to test my library, it's tedious but it works.

## Modal

As the library will show photos in fullscreen mode, we can just use [Modal](https://facebook.github.io/react-native/docs/modal.html) component provided by React Native. 

By passing `modalVisibility` prop with value `true`, we will show the `Modal`:

{{< highlight javascript >}}
<Modal transparent
  animationType={'fade'}
  visible={this.props.modalVisibility}
  >
  <View style={styles.wrapper}>
    <ImagePager navigationState={this.props.navigationState}
      closeModal={this.props.closeModal}
    />
  </View>
</Modal>
{{< /highlight >}}

Also, we need a `closeModal` function that child component will use to hide our fullscreen `Modal`:

{{< highlight javascript >}}
closeModal = () => {
  this.setState({
    modalVisibility: false
  })
}
render () {
  return (
    <ImageViewer modalVisibility={this.state.modalVisibility} closeModal={this.closeModal} />
  )
}
{{< /highlight >}}

## NavigationExperimental

Remember, the photos can be swiped through. We could take them as scenes managed by a navigator. Since `NavigationExperimental` will finally replace `Navigator` when it becomes stable, I would prefer using `NavigationExperimental` in this library.

The UIExplorer has [a great example](https://github.com/facebook/react-native/blob/master/Examples/UIExplorer/js/NavigationExperimental/NavigationTransitioner-AnimatedView-pager-example.js) showing how to make such a navigator with `NavigationExperimental`.

First, let's define a `navigationState` describing our photos state:

{{< highlight javascript >}}
{
  index: 0,
  routes: [
    {
      url: 'https://example.com/1.png'
    },
    {
      url: 'https://example.com/2.png'
    },
    {
      url: 'https://example.com/3.png'
    }
  ]
}
{{< /highlight >}}

`index` controls which route in `routes` should be activated. When we swipe through the photos, we're actually changing the `index` value in `navigationState`.

Of course we need to define [how to](https://github.com/chenxsan/react-native-image-viewer/blob/master/components/ImagePager.js#L8) update `navigationState`:

{{< highlight javascript >}}
function reducer (state, action) {
  switch (action) {
    case 'back':
      return NavigationStateUtils.back(state)
    case 'forward':
      return NavigationStateUtils.forward(state)
  }
  return state
}
{{< /highlight >}}

You should be familiar with the code if you had experience with [redux](https://github.com/reactjs/redux).

When a user swipes the photo, the library would dispatch `action` to update `navigationState`, and [scenes will be rerendered](https://github.com/chenxsan/react-native-image-viewer/blob/master/components/PagerNavigator.js#L42) as the `navigationState` in component changes.

You can check the gif image below:

![react-native-image-viewer](https://github.com/chenxsan/react-native-image-viewer/raw/master/react-native-image-viewer.gif)

If you want to check more, please go to my [github repository](https://github.com/chenxsan/react-native-image-viewer).