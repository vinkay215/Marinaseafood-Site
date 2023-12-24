var g_gmpAllMaps = [];
function gmpGetMembershipGmeViewId(map, oldViewId) {
	var newViewId = oldViewId;
	if(map && map.getParam && map.getParam('membershipEnable') == '1') {
		// prepare view id
		if(map._elementId && map._elementId.id && map._elementId.id.substr) {
			var viewIdKey = 'google_map_easy_'
			,	newIdPos = map._elementId.id.substr(viewIdKey.length);
			if(newIdPos) {
				newViewId = newIdPos;
			}
		}
	}
	return newViewId;
}
jQuery(document).ready(function(){
	var mapsInitClb = function() {
		if(typeof(gmpAllMapsInfo) !== 'undefined' && gmpAllMapsInfo && gmpAllMapsInfo.length) {
			for(var i = 0; i < gmpAllMapsInfo.length; i++) {
				if(jQuery('#'+ gmpAllMapsInfo[i].view_html_id).length) {
					gmpInitMapOnPage( gmpAllMapsInfo[i] );
				}
			}
			jQuery(document).trigger('gmpAmiVarInited');
		}
	};
	if(typeof(google) === 'undefined' 
		&& typeof(gmpLoadGoogleLib) !== 'undefined'	// Maybe it's just a static maps here - can do it without google lib
	) {
		gmpLoadGoogleLib();
		setTimeout(mapsInitClb, 1000);
	} else {
		mapsInitClb();
	}
});
function gmpInitMapOnPage(mapData) {
	if(mapData.params && parseInt(mapData.params.is_static) && typeof(gmpGoogleStaticMap) !== 'undefined') {
		new gmpGoogleStaticMap(mapData);
		return;
	}
	var additionalData = {
		markerGroups: typeof(mapData.marker_groups) != 'undefined' ? mapData.marker_groups : []
	}
	,	newMap = null
	,	mapMarkersIds = []
	,	markerIdToShow = gmpIsMarkerToShow()
	,	infoWndToShow = gmpIsInfoWndToShow();

	if(mapData && mapData.view_html_mbs_id) {
		// for membership Activity ajax load
		newMap = new gmpGoogleMap(mapData.view_html_mbs_id, mapData.params, additionalData);
		newMap.setParam('view_html_mbs_id', mapData.view_html_mbs_id);
		newMap.refreshWithCenter(mapData.params.center.lat(), mapData.params.center.lng(), mapData.params.zoom);
	} else {
		newMap = new gmpGoogleMap('#'+ mapData.view_html_id, mapData.params, additionalData);
	}

	// for membership Google Maps "Get original"
	if(mapData.mbs_presets == 1) {
		newMap.setParam('mbs_presets', 1);
	}

	if(mapData.markers && mapData.markers.length) {
		mapData.markers = _gmpPrepareMarkersList( mapData.markers );

		for(var i in mapData.markers) {
			mapMarkersIds.push(mapData.markers[i].id);
		}
		if(toeInArray(markerIdToShow, mapMarkersIds) == -1) {
			markerIdToShow = false;
		}
		if(toeInArray(infoWndToShow, mapMarkersIds) == -1) {
			infoWndToShow = false;
		}
		for(var j = 0; j < mapData.markers.length; j++) {
			if(markerIdToShow && mapData.markers[j].id != markerIdToShow) continue;
			if(infoWndToShow) {
				mapData.markers[j].params.show_description = mapData.markers[j].id == infoWndToShow ? '1' : '0';
			}
			var newMarker = newMap.addMarker( mapData.markers[j] );
			// We will set this only when marker info window need to be loaded
			/*newMarker.setTitle( mapData.markers[j].title, true );
			newMarker.setDescription( mapData.markers[j].description );*/
		}
		newMap.markersRefresh();
		newMap.checkMarkersParams(newMap.getAllMarkers(), markerIdToShow);
	}
	if(mapData.shapes && mapData.shapes.length) {
		mapData.shapes = _gmpPrepareShapesList( mapData.shapes );
		for(var z = 0; z < mapData.shapes.length; z++) {
			var newShape = newMap.addShape( mapData.shapes[z] );
		}
	}
	if(mapData.heatmap) {
		mapData.heatmap = _gmpPrepareHeatmapList( mapData.heatmap );
		newMap.addHeatmap( mapData.heatmap );
	}
	g_gmpAllMaps.push( newMap );
}
function gmpGetMapInfoById(id) {
	if(typeof(gmpAllMapsInfo) !== 'undefined' && gmpAllMapsInfo && gmpAllMapsInfo.length) {
		id = parseInt(id);
		for(var i = 0; i < gmpAllMapsInfo.length; i++) {
			if(gmpAllMapsInfo[i].id == id) {
				return gmpAllMapsInfo[i];
			}
		}
	}
	return false;
}
function gmpGetMapInfoByViewId(viewId) {
	if(typeof(gmpAllMapsInfo) !== 'undefined' && gmpAllMapsInfo && gmpAllMapsInfo.length) {
		for(var i = 0; i < gmpAllMapsInfo.length; i++) {
			if(gmpAllMapsInfo[i].view_id == viewId) {
				return gmpAllMapsInfo[i];
			}
		}
	}
	return false;
}
function gmpGetAllMaps() {
	return g_gmpAllMaps;
}
function gmpGetMapById(id) {
	var allMaps = gmpGetAllMaps();
	for(var i = 0; i < allMaps.length; i++) {
		if(allMaps[i].getId() == id) {
			return allMaps[i];
		}
	}
	return false;
}
function gmpGetMapByViewId(viewId) {
	var allMaps = gmpGetAllMaps();
	for(var i = 0; i < allMaps.length; i++) {
		var currViewId = allMaps[i].getViewId();
		if(window.gmpGetMembershipGmeViewId) {
			currViewId = gmpGetMembershipGmeViewId(allMaps[i], currViewId);
		}
		if(currViewId == viewId) {
			return allMaps[i];
		}
	}
	return false;
}
function gmpIsMarkerToShow() {
	var markerHash = 'gmpMarker'
	,	hashParams = toeGetHashParams();
	if(hashParams) {
		for(var i in hashParams) {
			if(!hashParams[i] || typeof(hashParams[i]) !== 'string') continue;
			var pair = hashParams[i].split('=');
			if(pair[0] == markerHash)
				return parseInt(pair[1]);
		}
	}
	return false;
}
function gmpIsInfoWndToShow() {
	var markerHash = 'gmpInfoWnd'
	,	hashParams = toeGetHashParams();
	if(hashParams) {
		for(var i in hashParams) {
			if(!hashParams[i] || typeof(hashParams[i]) !== 'string') continue;
			var pair = hashParams[i].split('=');
			if(pair[0] == markerHash)
				return parseInt(pair[1]);
		}
	}
	return false;
}