## Hi there 👋
<!--
I´m currently learning some programing and creating new ideas. 
Right now I´m with Java, SQL and a bit of JavaScript.
-->

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=900&size=15&duration=5061&pause=963&color=1E95F7&multiline=true&repeat=false&width=609&height=100&lines=I%C2%B4m+currently+learning+some+programing+and+creating+new+ideas.;Right+now+I%C2%B4m+with+Java%2C+SQL+and+a+bit+of+JavaScript.)](https://git.io/typing-svg)
name: generate animation

on:
  # run automatically every 24 hours
  schedule:
    - cron: "0 */6 * * *" 
  
  # allows to manually run the job at any time
  workflow_dispatch:
  
  # run on every push on the master branch
  push:
    branches:
    - master
    - main
    
  

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    
    steps:
      # generates a snake game from a github user (<github_user_name>) contributions graph, output a svg animation at <svg_out_path>
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          
          
      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
