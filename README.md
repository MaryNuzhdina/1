# 1
First code
name: Weekly Snapshot Release
on:
  schedule:
    - cron: '15 20 * * 0'
  workflow_dispatch: {}

jobs:
  create_release:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set snapshot tag
        id: set_snapshot_tag
        run: echo ::set-output name=tag::snapshot-$(date +'%Y-%m-%d')

      - name: Create release
        id: create_release
        uses: softprops/action-gh-release@v1
        with:
          generate_release_notes: true
          tag_name: ${{ steps.set_snapshot_tag.outputs.tag }}
          name: ${{ steps.set_snapshot_tag.outputs.tag }}
          draft: false
          prerelease: false
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}



// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    string public data;

    function setData(string memory _data) public {
        data = _data;
    }

    function getData() public view returns (string memory) {
        return data;
    }
}
