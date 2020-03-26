title: Home

# Electrolama!

Electrolama is a collection of open source projects and various other frivolities by [@OmerK](https://twitter.com/omerk) and friends.


# Changelog

(Pulled from the [docs repository](https://github.com/electrolama/docs/commits/master) with JavaScript, might be blank if you have it disabled)

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
      commit_details.href = commit.commit.url

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