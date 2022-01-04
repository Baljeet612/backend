# backendvar _ = require('lodash')
, data = require('world-countries')

module.exports = {
/**
* Determines whether a given international dialing code is valid
*
* @param string code
* @return bool
*/
isValid : function(code) {

var codes = _.flatten(_.pluck(data, 'callingCode'));

return _.contains(codes, code);

}
// ...
}

/**
* Gets a list of countries with the specified dialing code
*
* @param string code
* @return array An array of two-character country codes
*/
getCountries : function(code) {

var countryEntries = _.filter(data, function(country){
return (_.contains(country.callingCode, code));
})

return _.pluck(countryEntries, 'cca2');

}


/**
* Gets the dialing codes for a given country
*
* @param string country The two-character country code
* @return array An array of strings representing the dialing codes
*/
getCodes : function(country) {

// Get the country entry
var countryData = _.find(data, function(entry) {
return (entry.cca2 == country);
});

// Return the code(s)
return countryData.callingCode;

}

