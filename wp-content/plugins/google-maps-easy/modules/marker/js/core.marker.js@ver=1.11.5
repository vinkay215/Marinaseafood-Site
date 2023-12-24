// Markers
function gmpGoogleMarker(map, params) {
	this._map = map;
	this._markerObj = null;
	var defaults = {
		// Empty for now
	};
	if(!params.position && params.coord_x && params.coord_y) {
		params.position = new google.maps.LatLng(params.coord_x, params.coord_y);
	}
	this._markerParams = jQuery.extend({}, defaults, params);
	this._markerParams.map = this._map.getRawMapInstance();
	//this._id = params.id ? params.id : 0;
	this._infoWindow = null;
	this._infoWndOpened = false;
	this._infoWndWasInited = false;
	this._infoWndDirectionsBtn = false;
	this._infoWndPrintBtn = false;
	this._mapDragScroll = {
		scrollwheel: null
	};
	this.init();
}
gmpGoogleMarker.prototype.infoWndOpened = function() {
	return this._infoWndOpened;
};
gmpGoogleMarker.prototype.init = function() {
	var markerParamsForCreate = this._markerParams
	,	openInfoWndEvent = 'click'
	,	closeInfoWndEvent = ''
	,	openLinkEvent = 'click';

	if(parseInt(this._map._mapParams.hide_marker_tooltip)) {
		this._markerParams.marker_title = this._markerParams.title;
		delete markerParamsForCreate.title;
	}
	this._markerObj = new google.maps.Marker( markerParamsForCreate );
	if(this._markerParams.dragend) {
		this._markerObj.addListener('dragend', jQuery.proxy(this._markerParams.dragend, this));
	}
	if(this._markerParams.click) {
		this._markerObj.addListener('click', jQuery.proxy(this._markerParams.click, this));
	}
	this._markerObj.addListener('domready', jQuery.proxy(function(){
		changeInfoWndBgColor(this._map);
	}, this));
	if(this._markerParams.params && !(window.ontouchstart === null || navigator.msMaxTouchPoints)) {
		if(parseInt(this._markerParams.params.description_mouse_hover)) {
			openInfoWndEvent = 'mouseover';
			if(parseInt(this._markerParams.params.description_mouse_leave)) {
				closeInfoWndEvent = 'mouseout';
			}
		}
	}
	this._markerObj.addListener(openInfoWndEvent, jQuery.proxy(function () {
		if(this._markerParams.params
			&& !parseInt(this._markerParams.params.description_mouse_hover)
			&& parseInt(this._markerParams.params.marker_link)
		) {
			return;
		} else {
			this.showInfoWnd();
		}
        jQuery(document).trigger('gmapAfterMarkerClick', this);
	}, this));
	if(closeInfoWndEvent) {
		this._markerObj.addListener(closeInfoWndEvent, jQuery.proxy(function () {
			var self = this
			,	infoWndDiv = jQuery('.gm-style-iw').parent()
			,	timeout = 300;

			infoWndDiv.on('mouseover', function () {
				// Mouse is on infowindow content
				infoWndDiv.addClass('hovering');
			});
			infoWndDiv.on('mouseleave', function () {
				// Hide infowindow after mouse have left infowindow content
				setTimeout(function() {
					self.hideInfoWnd();
				}, timeout);
			});
			setTimeout(function() {
				// Hide infowindow if mouse is not on infowindow content
				if(!infoWndDiv.hasClass('hovering')) {
					self.hideInfoWnd();
				}
			}, timeout);
		}, this));
	}
	if(this._markerParams.params && parseInt(this._markerParams.params.marker_link)) {
		this._markerObj.addListener(openLinkEvent, jQuery.proxy(function () {
			var isLink = /http/gi
			,	markerLink = !this._markerParams.params.marker_link_src.match(isLink)
					? 'http://' + this._markerParams.params.marker_link_src
					: this._markerParams.params.marker_link_src;

			if(parseInt(this._markerParams.params.marker_link_new_wnd)) {
				window.open(markerLink,	'_blank');
			} else {
				location.href = markerLink;
			}
		}, this));
	}
};
gmpGoogleMarker.prototype.showInfoWnd = function( forceUpdateInfoWnd, forceShow ) {
	var allShapes = this._map.getAllShapes();
	if(allShapes && allShapes.length) {
		for(var i = 0; i < allShapes.length; i++) {
			if(allShapes[i]._infoWndOpened) allShapes[i].hideInfoWnd();
		}
	}
	if(!this._infoWndWasInited || forceUpdateInfoWnd) {
		this._updateInfoWndContent();
		this._infoWndWasInited = true;
	}
	if(this._infoWindow && !this._infoWndOpened) {
		var allMapMArkers = this._map.getAllMarkers();
		// Google Maps Javascript API v3 allows to open several infowindows on map
		if(allMapMArkers && allMapMArkers.length > 1 && !forceShow) {
			for(var i = 0; i < allMapMArkers.length; i++) {
				allMapMArkers[i].hideInfoWnd();
			}
		}
		if(parseInt(this.getMap().getParam('center_on_cur_marker_infownd')) && !GMP_DATA.isAdmin) {
			this.getMap().setCenter(this.getMarkerParam('position'));
		}
		if(this._map.getParam('marker_infownd_type') == 'slide' && (typeof(this.showInfoWndSlide) == 'function')) {
			this.showInfoWndSlide();
		} else {
			this._infoWindow.open(this._map.getRawMapInstance(), this._markerObj);
		}
		this._infoWndOpened = true;
	}
};
gmpGoogleMarker.prototype.hideInfoWnd = function() {
	if(this._infoWindow && this._infoWndOpened) {
		this._infoWindow.close();
		this._infoWndOpened = false;

		var googleMap = this._map.getRawMapInstance();
		googleMap.setOptions( {scrollwheel: this._mapDragScroll.scrollwheel} );

		jQuery(document).trigger('gmapAfterHideInfoWnd', this);
	}
};
gmpGoogleMarker.prototype.getRawMarkerInstance = function() {
	return this._markerObj;
};
gmpGoogleMarker.prototype.getRawMarkerParams = function() {
	return this._markerParams;
};
gmpGoogleMarker.prototype.getIcon = (function() {
	return this._markerObj.getIcon();
});
gmpGoogleMarker.prototype.setIcon = function(iconPath) {
	this._markerObj.setIcon( iconPath );
};
gmpGoogleMarker.prototype.setTitle = function(title, noRefresh) {
	if(!parseInt(this._map._mapParams.hide_marker_tooltip))
		this._markerObj.setTitle( title );
	this._markerParams.title = title;
	if(!noRefresh)
		this._updateInfoWndContent();
};
gmpGoogleMarker.prototype.getTitle = function() {
	return typeof this._markerParams.title != 'undefined' ? this._markerParams.title : this._markerParams.marker_title;
};
gmpGoogleMarker.prototype.getPosition = function() {
	return this._markerObj.getPosition();
};
gmpGoogleMarker.prototype.setPosition = function(lat, lng) {
	this._markerObj.setPosition( new google.maps.LatLng(lat, lng) );
};
gmpGoogleMarker.prototype.lat = function() {
	return this.getPosition().lat();
};
gmpGoogleMarker.prototype.lng = function(lng) {
	return this.getPosition().lng();
};
gmpGoogleMarker.prototype.setId = function(id) {
	this._markerParams.id = id;
};
gmpGoogleMarker.prototype.getId = function() {
	return this._markerParams.id;
};
gmpGoogleMarker.prototype.setDescription = function (description, noRefresh) {
	this._markerParams.description = description;
	if(!noRefresh)
		this._updateInfoWndContent();
	if(this._markerParams.params && parseInt(this._markerParams.params.show_description)) {
		this.showInfoWnd(false, true);
	}
};
gmpGoogleMarker.prototype.getDescription = function () {
	return this._markerParams.description;
};
gmpGoogleMarker.prototype._setTitleColor = function(titleDiv) {
	var titleColor = this._map.getParam('marker_title_color');

	if(titleColor && titleColor != '') {
		titleDiv.css({
			'color': titleColor
		});
	}
	return titleDiv;
};
gmpGoogleMarker.prototype._setTitleSize = function(titleDiv) {
	var titleSize = this._map.getParam('marker_title_size')
	,	titleSizeUnits = this._map.getParam('marker_title_size_units');

	if(titleSize && titleSizeUnits && titleSize != '') {
		titleDiv.css({
			'font-size': titleSize + titleSizeUnits
		,	'line-height': (+titleSize + 5) + titleSizeUnits
		});
	}
	return titleDiv;
};
gmpGoogleMarker.prototype._setDescSize = function(descDiv) {
	var descSize = this._map.getParam('marker_desc_size')
	,	descSizeUnits = this._map.getParam('marker_desc_size_units');

	if(descSize && descSizeUnits && descSize != '') {
		descDiv.css({
			'font-size': descSize + descSizeUnits
		,	'line-height': parseInt(descSize) + 5 + descSizeUnits
		});
	}
	return descDiv;
};
gmpGoogleMarker.prototype._updateInfoWndContent = function() {
	var contentStr = jQuery('<div/>', {})
	,	description = this._markerParams.description ? this._markerParams.description.replace(/\n/g, '<br/>') : false
	,	title = this._markerParams.title ? this._markerParams.title : false;

	if(parseInt(this._map._mapParams.hide_marker_tooltip) && !GMP_DATA.isAdmin) {
		title = this._markerParams.marker_title ? this._markerParams.marker_title : false;
	}
	if(title) {
		var titleDiv = jQuery('<div/>', {})
			.addClass('gmpInfoWindowtitle')
			.html( title );

		titleDiv = this._setTitleColor(titleDiv);
		titleDiv = this._setTitleSize(titleDiv);
		contentStr.append( titleDiv );

		if(this._infoWndDirectionsBtn) {
			this._infoWndDirectionsBtn.insertAfter(contentStr.find('.gmpInfoWindowtitle'));
		}
		if(this._infoWndPrintBtn) {
			this._infoWndPrintBtn.insertAfter(contentStr.find('.gmpInfoWindowtitle'));
		}
	}
	if(description) {
		var descDiv = jQuery('<div/>', {})
			.addClass('egm-marker-iw')
			.html( description );

		descDiv = this._setDescSize(descDiv);
		contentStr.append( descDiv );

		// Check scripts in description, and execute them if they are there
		var $scripts = contentStr.find('script');
		if($scripts && $scripts.length) {
			$scripts.each(function(){
				var scriptSrc = jQuery(this).attr('src');
				if(scriptSrc && scriptSrc != '') {
					jQuery.getScript( scriptSrc );
				}
			});
		}
	}
	this._setInfoWndContent( contentStr );
};
/**
 * Just mark it as closed
 */
gmpGoogleMarker.prototype._setInfoWndClosed = function() {
	this._infoWndOpened = false;
	jQuery(document).trigger('gmapAfterHideInfoWnd', this);
};
gmpGoogleMarker.prototype._setInfoWndContent = function(newContentHtmlObj) {
	var self = this
	,	map = this.getMap();

	if(!this._infoWindow) {
		var mapWidth = GMP_DATA.isAdmin ? jQuery('#gmpMapPreview').width() : jQuery('#' + map.getViewHtmlId()).width()
		,	infoWndType = map.getParam('marker_infownd_type')
		,	infoWndWidth = map.getParam('marker_infownd_width_units') == 'px' ? map.getParam('marker_infownd_width') : mapWidth - 20
		,	infoWndHeight = map.getParam('marker_infownd_height_units') == 'px' ? map.getParam('marker_infownd_height')+ 'px' : false
		,	maxWndWidth = mapWidth * 0.6
		,	infoWndParams = { maxWidth: infoWndWidth < maxWndWidth ? infoWndWidth : maxWndWidth };

		switch(infoWndType) {
			case 'rounded_edges':
				infoWndParams.pixelOffset = new google.maps.Size(0, 10);
				break;
			default:
				break;
		}

		//add disableAutoPan property if description_mouse_leave is true
		/*if(this._markerParams.params && this._markerParams.params.description_mouse_leave)
			infoWndParams['disableAutoPan'] = true;*/

		this._infoWindow = new google.maps.InfoWindow(infoWndParams);

		google.maps.event.addListener(this._infoWindow, 'domready', function(){
			changeInfoWndType(map);
			changeInfoWndBgColor(map);
			// check if tooltip text has "Gallery by Supsystic"
			if(this.content && this.content.innerHTML && this.content.innerHTML.indexOf && this.content.innerHTML.indexOf('id="grid-gallery-') != -1) {
				jQuery(document).trigger('ggFirInitialize');
			}
		});
		google.maps.event.addListener(this._infoWindow, 'closeclick', function(){
			self._setInfoWndClosed();
		});
	}
	if(infoWndHeight) {
		newContentHtmlObj.css('cssText', 'max-height: '+ infoWndHeight +';');
	}

	// Fix bug in FF - scroll on infowindow content changes map zoom
	var scrollwheel = map.get('scrollwheel')
	,	googleMap = map.getRawMapInstance();

	//Save scrollwheel setting to container before rewrite it.
	this._mapDragScroll.scrollwheel = scrollwheel;

	newContentHtmlObj.hover(
		function() {
			googleMap.setOptions({ scrollwheel: false });
		},
		function() {
			googleMap.setOptions({ scrollwheel: scrollwheel });
		}
	);
	this._infoWindow.setContent(newContentHtmlObj[0]);
};
gmpGoogleMarker.prototype.removeFromMap = function() {
	this.getRawMarkerInstance().setMap( null );
};
gmpGoogleMarker.prototype.setMarkerParams = function(params) {
	this._markerParams = params;
	return this;
};
gmpGoogleMarker.prototype.setMarkerParam = function(key, value) {
	this._markerParams[ key ] = value;
	return this;
};
gmpGoogleMarker.prototype.getMarkerParam = function(key) {
	return this._markerParams[ key ];
};
gmpGoogleMarker.prototype.setMap = function( map ) {
	this.getRawMarkerInstance().setMap( map );
};
gmpGoogleMarker.prototype.getMap = function() {
	return this._map;
};
gmpGoogleMarker.prototype.setVisible = function(state) {
	this.getRawMarkerInstance().setVisible(state);
}
gmpGoogleMarker.prototype.getVisible = function(state) {
	this.getRawMarkerInstance().getVisible(state);
}
// Common functions
function _gmpPrepareMarkersList(markers, params) {
	params = params || {};
	if(markers) {
		for(var i = 0; i < markers.length; i++) {
			markers[i].coord_x = parseFloat( markers[i].coord_x );
			markers[i].coord_y = parseFloat( markers[i].coord_y );
			markers[i].icon = markers[i].icon_data.path;
			if(params.dragend) {
				markers[i].draggable = true;
				markers[i].dragend = params.dragend;
			}
		}
	}
	return markers;
}

window.gmpGoogleMarker = gmpGoogleMarker;
