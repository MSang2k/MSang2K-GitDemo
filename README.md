import QtQuick 2.15
import QtQuick.Controls 2.3

Page {
    signal login(string username,string password)

    property string checkUsername: ""
    property string checkPassword: "1"
    property string status: "Failed"

    property real textWidth : 230
    property real textHeight : 50
    property real globalSpacing : 10
    property real globalBorder: 2
    property real sizeButton: 230
    property real radiusButton: sizeButton

    id: loginPage

    Popup {
        id: statusPopup
        closePolicy: Popup.CloseOnEscape | Popup.CloseOnPressOutside
        anchors.centerIn: parent
        width: recLabelPop.Width
        height: recLabelPop.Height
        modal: true
        focus: true

        Rectangle {
            id: recLabelPop
            width: statusLabel.contentWidth + globalSpacing
            height: statusLabel.contentHeight + globalSpacing
            anchors.centerIn: parent

            Label {
                id: statusLabel
                anchors.centerIn: parent
                text: status
                font.bold: true
            }
        }

        Timer {
            id:timer
            interval: 2000; running: true; repeat: true
            onTriggered: {
                statusPopup.close()
                timer.stop()
            }
        }
    }

    Popup {
        id: regisPopup
        closePolicy: Popup.CloseOnEscape | Popup.CloseOnPressOutside
        anchors.centerIn: parent
        width: gridPop.implicitWidth + globalSpacing*2
        height: gridPop.implicitHeight + recMouse0.height + globalSpacing*4
        modal: true
        focus: true

        Column {
            id: columnPop
            anchors.verticalCenter: parent.verticalCenter
            anchors.horizontalCenter: parent.horizontalCenter
            spacing: globalSpacing

            Rectangle {
                width: gridPop.implicitWidth
                height: gridPop.implicitHeight

                Grid {
                    id: gridPop
                    spacing: globalSpacing
                    columns: 2

                    // Enter user name
                    Rectangle {
                        width: labelRegisUser.contentWidth
                        height: txtRegisUsername.height

                        Label {
                            id: labelRegisUser
                            anchors.centerIn: parent
                            text: qsTr("Username")
                        }
                    }

                    Rectangle {
                        width: textWidth
                        height: textHeight
                        radius: textWidth
    //                    border.color: "#12CBC4"
                        border.width: globalBorder
                        antialiasing: true
                        clip: true

                        TextInput {
                            id: txtRegisUsername
                            text: qsTr("")
                            anchors.fill: parent
                            verticalAlignment: TextInput.AlignVCenter
                            anchors.leftMargin: globalSpacing
    //                        color: "#55E6C1"
    //                        font.family: "Helvetica"
    //                        font.bold: true
                            selectByMouse: true
                            activeFocusOnTab: true
                            focus: true
                            Keys.onReturnPressed: txtRegisPassword.focus = true

                        }
                    }

                    // Enter password
                    Rectangle {
                        width: labelRegisPass.contentWidth
                        height: txtRegisPassword.height

                        Label {
                            id: labelRegisPass
                            anchors.centerIn: parent
                            text: qsTr("Password")
                        }
                    }

                    Rectangle {
                        width: textWidth
                        height: textHeight
                        radius: textWidth
                        border.width: globalBorder
                        clip: true

                        TextInput {
                            id: txtRegisPassword
                            text: qsTr("")
                            anchors.fill: parent
                            verticalAlignment: TextInput.AlignVCenter
                            anchors.leftMargin: globalSpacing
                            selectByMouse: true
                            activeFocusOnTab: true
                            focus: true
                            echoMode: TextInput.Password
                        }
                    }

                    // Enter password
                    Rectangle {
                        width: labelRePass.contentWidth
                        height: txtRegisPassword.height

                        Label {
                            id: labelRePass
                            anchors.centerIn: parent
                            text: qsTr("Re-Password")
                        }
                    }

                    Rectangle {
                        width: textWidth
                        height: textHeight
                        radius: textWidth
                        border.width: globalBorder
                        clip: true

                        TextInput {
                            id: txtRePassword
                            text: qsTr("")
                            anchors.fill: parent
                            verticalAlignment: TextInput.AlignVCenter
                            anchors.leftMargin: globalSpacing
                            selectByMouse: true
                            activeFocusOnTab: true
                            focus: true
                            echoMode: TextInput.Password
                            Keys.onEnterPressed: login(txtUsername.text, txtPassword.text)
                            Keys.onReturnPressed: login(txtUsername.text, txtPassword.text)
                        }
                    }
                }
            }

            Rectangle {
                id: recMouse0
                width:sizeButton
                height: sizeButton/5
                x: labelPass.contentWidth + globalSpacing
                radius: radiusButton
                color:  "#17A589"

                Label {
                    anchors.centerIn: parent
                    text: qsTr("Create")
                    color: "white"
                    font.bold: true
                }

                MouseArea {
                    anchors.fill: parent
                    hoverEnabled: true
                    onEntered: parent.color = "#76D7C4"
                    onExited: parent.color = "#17A589"
                    onClicked:{
                        login(txtUsername.text, txtPassword.text)
                    }
                }
            }
        }
    }

    Column {
        id: column
        width: loginPage.width/2
        height: loginPage.height/2
        anchors.verticalCenter: parent.verticalCenter
        anchors.horizontalCenter: parent.horizontalCenter
        spacing: globalSpacing

        Rectangle {
            width: grid.implicitWidth
            height: grid.implicitHeight

            Grid {
                id: grid
                spacing: globalSpacing
                columns: 2

                // Enter user name
                Rectangle {
                    width: labelUser.contentWidth
                    height: txtUsername.height

                    Label {
                        id: labelUser
                        anchors.centerIn: parent
                        text: qsTr("Username")
                    }
                }

                Rectangle {
                    width: textWidth
                    height: textHeight
                    radius: textWidth
                    border.width: globalBorder
                    antialiasing: true
                    clip: true

                    TextInput {
                        id: txtUsername
                        text: qsTr("")
                        anchors.fill: parent
                        verticalAlignment: TextInput.AlignVCenter
                        anchors.leftMargin: globalSpacing
                        selectByMouse: true
                        activeFocusOnTab: true
                        focus: true
                        Keys.onReturnPressed: txtPassword.focus = true

                    }
                }

                // Enter password
                Rectangle {
                    width: labelPass.contentWidth
                    height: txtPassword.height

                    Label {
                        id: labelPass
                        anchors.centerIn: parent
                        text: qsTr("Password")
                    }
                }

                Rectangle {
                    width: textWidth
                    height: textHeight
                    radius: textWidth
                    border.width: globalBorder
                    clip: true

                    TextInput {
                        id: txtPassword
                        text: qsTr("")
                        anchors.fill: parent
                        verticalAlignment: TextInput.AlignVCenter
                        anchors.leftMargin: globalSpacing
                        selectByMouse: true
                        activeFocusOnTab: true
                        focus: true
                        echoMode: TextInput.Password
                        Keys.onEnterPressed: login(txtUsername.text, txtPassword.text)
                        Keys.onReturnPressed: login(txtUsername.text, txtPassword.text)
                    }
                }

            }
        }

        Rectangle {
            id: recMouse1
            width:sizeButton
            height: sizeButton/5
            x: labelPass.contentWidth + globalSpacing
            radius: radiusButton
            color:  "#17A589"

            Label {
                anchors.centerIn: parent
                text: qsTr("Log In")
                color: "white"
                font.bold: true
            }

            MouseArea {
                anchors.fill: parent
                hoverEnabled: true
                onEntered: parent.color = "#76D7C4"
                onExited: parent.color = "#17A589"
                onClicked:{
                    login(txtUsername.text, txtPassword.text)
                }
            }
        }

        Rectangle {
            id: recMouse
            width:sizeButton
            height: sizeButton/5
            x: labelPass.contentWidth + globalSpacing
            radius: radiusButton
            color:  "#ff0080"

            Label {
                anchors.centerIn: parent
                text: qsTr("Create new account")
                color: "white"
                font.bold: true
            }

            MouseArea {
                anchors.fill: parent
                hoverEnabled: true
                onEntered: parent.color = "#ff66b3"
                onExited: parent.color = "#ff0080"
                onClicked:{
                    regisPopup.open()
                }
            }
        }
    }

    onLogin:{
        if(username === checkUsername  && password === checkPassword){
            status = "Hello!"
        }else{
            status = "\tLog in failed\n Usernam or Password is incorrect"
        }
        statusPopup.open()
        timer.start()
    }
}
