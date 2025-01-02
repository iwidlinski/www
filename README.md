# widlinski.github.io

# download the theme
hugo mod get -u
# download the theme's dependencies
hugo mod tidy
# generate node dependencies
hugo mod npm pack
# install install dependencies
npm install