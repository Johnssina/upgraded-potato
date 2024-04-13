// Example script for a farmer job in SA-MP

#include <a_samp>

new const Float:FIELD_X = 100.0, FIELD_Y = 200.0, FIELD_Z = 15.0; // Coordinates of the farm field
new const Float:HARVEST_DISTANCE = 5.0; // Maximum distance for harvesting crops
new const Float:CROP_PRICE = 10.0; // Price per unit of harvested crop

public OnPlayerCommandText(playerid, cmdtext[]) {
    if (strcmp(cmdtext, "/startfarming", true) == 0) {
        StartFarming(playerid);
        return 1;
    }
    if (strcmp(cmdtext, "/harvest", true) == 0) {
        HarvestCrops(playerid);
        return 1;
    }
    return 0;
}

public StartFarming(playerid) {
    // Teleport the player to the farm field
    SetPlayerPos(playerid, FIELD_X, FIELD_Y, FIELD_Z);
    SendClientMessage(playerid, COLOR_YELLOW, "You are now at the farm field. Start planting crops with /plant.");
}

public HarvestCrops(playerid) {
    // Check if the player is near the farm field
    if (GetPlayerDistanceFromPoint(playerid, FIELD_X, FIELD_Y, FIELD_Z) <= HARVEST_DISTANCE) {
        // Calculate the number of crops harvested
        new crops = Random(10, 20); // Random number of crops between 10 and 20

        // Give the player money for harvested crops
        GivePlayerMoney(playerid, crops * CROP_PRICE);
        SendClientMessage(playerid, COLOR_YELLOW, "You harvested " + crops + " crops and earned $" + (crops * CROP_PRICE) + ".");
    } else {
        SendClientMessage(playerid, COLOR_RED, "You are not near the farm field. Get closer to harvest crops.");
    }
}

