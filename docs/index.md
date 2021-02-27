title: Home

# Electrolama!

Electrolama is a collection of open source projects and various other frivolities by [@OmerK](https://twitter.com/omerk) and friends.


## Changelog

<ul id="commits"></ul>

<script>
document.addEventListener( "DOMContentLoaded", function(event) {

  let url = 'https://api.github.com/repos/electrolama/docs/commits';

  fetch(url)
  .then(res => res.json())
  .then( (out) => {

    var commits_list = document.getElementById("commits");

    commits = out.slice(0, 10)
    commits.forEach( function(commit, index){

      var commit_date = new Date(commit.commit.author.date)
      var commit_details = document.createElement('a');
      commit_details.appendChild( document.createTextNode(commit.commit.message) )
      commit_details.href = commit.html_url

      var li = document.createElement("li");
      li.appendChild( document.createTextNode(commit_date.toLocaleDateString() + " - ") )
      li.appendChild(commit_details)
      li.appendChild( document.createTextNode(" (" + commit.author.login + ")") )
      commits_list.appendChild(li);

    } );

  } )
  .catch(err => { throw err });
  
} );
</script>

![Under Construction](_assets/under_construction.gif) Perpetually under construction 


## Contact 

For general enquiries, suggestions and errors spotted: Email us at [hello@electrolama.com](mailto:hello@electrolama.com). Community contributions to these pages are very much encouraged so you could also send pull requests on the [documentation repo](https://github.com/electrolama/docs) (source of these pages) with your proposed changes.

For support regarding Tindie purchases: [support@electrolama.com](mailto:support@electrolama.com). Please note that we do not monitor Github issues or third party forums for customer support.

## License
This repository (contents of [electrolama.com](https://electrolama.com), documentation for Electrolama projects) is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/). 

For specific licenses that apply to Electrolama hardware projects, please see license notices in relevant repositories.
