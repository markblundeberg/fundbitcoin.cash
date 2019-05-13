---
title: Home
type: docs
---
<script src="https://code.jquery.com/jquery-3.3.1.min.js" integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8=" crossorigin="anonymous"></script>

## Projects

<table>
<thead>
<tr>
    <th rowspan="2">Project</th>
    <th>Developer</th>
    <th>QR Code</th>
    <th></th>
</tr>
</thead>
<tbody>
<!--- Bitcoin ABC ---> 
<tr>
    <td rowspan="2">
    Bitcoin-ABC
    </td>
    <td>
        Amaury Sechet
    </td>
    <td rowspan="2">
        <img src="abc-addr.png" height="128"/>
    </td>
    <td rowspan="2">
        <button class="badger-button" data-text="Donate $1" data-to="bitcoincash:qqeht8vnwag20yv8dvtcrd4ujx09fwxwsqqqw93w88">
          <span>Donate</span>
        </button>
    </td>
</tr>
<tr>
    <td>
        <a href="https://blockdozer.com/address/qqeht8vnwag20yv8dvtcrd4ujx09fwxwsqqqw93w88">
        qqeht8vnwag20yv8dvtcrd4ujx09fwxwsqqqw93w88
        </a>
    </td>
</tr>
<!--- Electron Cash ---> 
<tr>
    <td rowspan="2">
        <a href="https://electroncash.org/">Electron Cash</a>
    </td>
    <td>
        Jonald Fyookball
    </td>
    <td rowspan="2">
        <img src="ec-addr.png" height="128"/>
    </td>
    <td rowspan="2">
        <button class="badger-button" data-text="Donate $1" data-to="bitcoincash:qz4wq9m860zr5p2nfdpttm5ymdqdyt3psc95qjagae">
          <span>Donate</span>
        </button>
    </td>
</tr>
<tr>
    <td>
        <a href="https://blockdozer.com/address/qz4wq9m860zr5p2nfdpttm5ymdqdyt3psc95qjagae">
        qz4wq9m860zr5p2nfdpttm5ymdqdyt3psc95qjagae
        </a>
    </td>
</tr>
<!--- bchd ---> 
<tr>
    <td rowspan="2">
        bchd
    </td>
    <td>
        Chris Pacia
    </td>
    <td rowspan="2">
        <img src="bchd-addr.png" height="128"/>
    </td>
    <td rowspan="2">
        <button class="badger-button" data-text="Donate $1" data-to="bitcoincash:qrhea03074073ff3zv9whh0nggxc7k03ssh8jv9mkx">
          <span>Donate</span>
        </button>
    </td>
</tr>
<tr>
    <td>
        <a href="https://blockdozer.com/address/qrhea03074073ff3zv9whh0nggxc7k03ssh8jv9mkx">
        qrhea03074073ff3zv9whh0nggxc7k03ssh8jv9mkx
        </a>
    </td>
</tr>
<!--- Crescent Cash ---> 
<tr>
    <td rowspan="2">
        Crescent Cash
    </td>
    <td>
        pokkst
    </td>
    <td rowspan="2">
        <img src="crescent-cash-addr.png" height="128"/>
    </td>
    <td rowspan="2">
        <button class="badger-button" data-text="Donate $1" data-to="bitcoincash:qptnypuugy29lttleggl7l0vpls0vg295q9nsavw6g">
          <span>Donate</span>
        </button>
    </td>
</tr>
<tr>
    <td>
        <a href="https://blockdozer.com/address/qptnypuugy29lttleggl7l0vpls0vg295q9nsavw6g">
        qptnypuugy29lttleggl7l0vpls0vg295q9nsavw6g
        </a>
    </td>
</tr>
<!--- end --->
</tbody>
</table>

<script>
// Tree fiddy
defaultDonation = 3.50;

function getBCHPrice () {
  return new Promise((resolve, reject) => {
    jQuery.getJSON('https://index-api.bitcoin.com/api/v0/cash/price/usd', function (result) {
      if (result.price != '') {
        var singleDollarValue = result.price / 100;
        var singleDollarSatoshis = 100000000 / singleDollarValue * defaultDonation;
        resolve(singleDollarSatoshis);
      } else {
        reject(new Error(result.error));
      }
    });
  });
};
jQuery(window).on('load', function(){ 
  getBCHPrice().then(function(res) {
    var badgerButtons = document.body.getElementsByClassName("badger-button")
    for (var i = 0; i < badgerButtons.length; i++) {
      var badgerButton = badgerButtons[i]
      badgerButton.addEventListener('click', function(event) {
        if (typeof web4bch !== 'undefined') {
          web4bch = new Web4Bch(web4bch.currentProvider)
          var txParams = {
            to: badgerButton.getAttribute("data-to"),
            from: web4bch.bch.defaultAccount,
            value: res
          }
          web4bch.bch.sendTransaction(txParams, (err, res) => {
            if (err) return
            var paywallId = badgerButton.getAttribute("data-paywall-id")
            if (paywallId) {
              var paywall = document.getElementById("paywall")
              paywall.style.display = "block"
            }
            var successCallback = badgerButton.getAttribute("data-success-callback")
            if (successCallback) {
              window[successCallback](res)
            }
          })
        } else {
          window.open('https://badgerwallet.cash')
        }
      })
    }
  });
});
</script>
