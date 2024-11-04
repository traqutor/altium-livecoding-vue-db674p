Hello stranger!

During this challenge you need to implement a simple application displaying fetched comments as circles ala Figma.

Data to be rendered is operated by the endpoint (https://puelle.me/api/comments). But beware — the default response type is `text/x-yaml`, `application/json` is supported though, the stranger just need to figure out how to make the endpoint respond like that.

The app should render gotten comments as circles with the following stats:

- 32 by 32 px
- transparent background
- colored 2px border (`color` may be found in the API)
- content is `id` colored with `color`
- content must be centered inside of the circle

Positioning is tricky though. Coordinates `position` from the API are not px but abstract units. Consider the screen as a canvas with dimensions 600x600. So a comment with `position` `[300, 300]` must be in the center of any dimensional screen.
