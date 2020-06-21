/* eslint-disable */
<template>
  <div>
    <!--<base-header type="gradient-success" class="pb-6 pb-8 pt-5 pt-md-8">
        &lt;!&ndash; Card stats &ndash;&gt;
        <div class="row">
            <div class="col-xl-3 col-lg-6">
                <stats-card title="Total traffic"
                            type="gradient-red"
                            sub-title="350,897"
                            icon="ni ni-active-40"
                            class="mb-4 mb-xl-0"
                >

                    <template slot="footer">
                        <span class="text-success mr-2"><i class="fa fa-arrow-up"></i> 3.48%</span>
                        <span class="text-nowrap">Since last month</span>
                    </template>
                </stats-card>
            </div>
            <div class="col-xl-3 col-lg-6">
                <stats-card title="Total traffic"
                            type="gradient-orange"
                            sub-title="2,356"
                            icon="ni ni-chart-pie-35"
                            class="mb-4 mb-xl-0"
                >

                    <template slot="footer">
                        <span class="text-success mr-2"><i class="fa fa-arrow-up"></i> 12.18%</span>
                        <span class="text-nowrap">Since last month</span>
                    </template>
                </stats-card>
            </div>
            <div class="col-xl-3 col-lg-6">
                <stats-card title="Sales"
                            type="gradient-green"
                            sub-title="924"
                            icon="ni ni-money-coins"
                            class="mb-4 mb-xl-0"
                >

                    <template slot="footer">
                        <span class="text-danger mr-2"><i class="fa fa-arrow-down"></i> 5.72%</span>
                        <span class="text-nowrap">Since last month</span>
                    </template>
                </stats-card>

            </div>
            <div class="col-xl-3 col-lg-6">
                <stats-card title="Performance"
                            type="gradient-info"
                            sub-title="49,65%"
                            icon="ni ni-chart-bar-32"
                            class="mb-4 mb-xl-0"
                >

                    <template slot="footer">
                        <span class="text-success mr-2"><i class="fa fa-arrow-up"></i> 54.8%</span>
                        <span class="text-nowrap">Since last month</span>
                    </template>
                </stats-card>
            </div>
        </div>
    </base-header>-->

    <!--Charts-->
    <div class="container-fluid mt-5">
      <div class="row">
        <div class="col-xl-8 mb-5 mb-xl-0">
          <card header-classes="bg-transparent">
            <div slot="header" class="row align-items-center">
              <div class="col">
                <!--<h6 class="text-light text-uppercase ls-1 mb-1">Overview</h6>-->
                <h5 class="h3 mb-0">File upload</h5>
              </div>
              <div class="col">
                <ul class="nav nav-pills justify-content-end">
                  <li class="nav-item mr-2 mr-md-0">
                    <a class="nav-link py-2 px-3 active btn btn-link" @click="clearUploads">
                                            <span class="d-none d-md-block"><i class="ni ni-scissors"
                                                                               aria-hidden="true"></i> clear</span>
                      <span class="d-md-none">x</span>
                    </a>
                  </li>
                  <li class="nav-item">
                    <a class="nav-link py-2 px-3"
                       href="#"
                       @click="modal0 = true"
                       :class="{active: bigLineChart.activeIndex === 1}">
                      <span class="d-none d-md-block"><i class="ni ni-money-coins"></i> Financial</span>
                      <span class="d-md-none"><i class="ni ni-money-coins"></i></span>
                    </a>
                  </li>
                </ul>
              </div>
            </div>
            <!--<line-chart
                    :height="350"
                    ref="bigChart"
                    :chart-data="bigLineChart.chartData"
                    :extra-options="bigLineChart.extraOptions"
            >
            </line-chart>-->

            <vue-dropzone
                ref="blueDropZone"
                id="dropzone"
                :options="dropzoneOptions"
                @vdropzone-complete="uploadCompleted"
                @vdropzone-success="uploadSuccess"
                @vdropzone-error="uploadFailed"
                @vdropzone-file-added="processingFile"
            ></vue-dropzone>

          </card>
        </div>

        <div class="col-xl-4">
          <card header-classes="bg-transparent">
            <div slot="header" class="row align-items-center">
              <div class="col">
                <h6 class="text-uppercase text-muted ls-1 mb-1">Performance</h6>
                <h5 class="h3 mb-0">Uploaded files</h5>
              </div>
            </div>

            <!--<bar-chart
                    :height="350"
                    ref="barChart"
                    :chart-data="redBarChart.chartData"
            >
            </bar-chart>-->

            <div>
              <ul class="list-group list-group-flush" v-for="upload in uploads"
                  v-bind:key="upload">
                <li class="list-group-item">
                  <div class="col">
                    <h6 class="text-uppercase mb-1"> {{ upload.tempFileName }}</h6>
                    <h6 class="text-muted mb-1">{{ upload.uploadMessage }}</h6>
                    <div class="progress" v-if="upload.uploadStatus">
                      <div class="progress-bar progress-bar-striped progress-bar-animated bg-info"
                           role="progressbar"
                           style="width: 100%"
                           aria-valuenow="100"
                           aria-valuemin="0"
                           aria-valuemax="100"
                      ></div>
                    </div>
                  </div>
                </li>
              </ul>
            </div>

          </card>
        </div>
      </div>
      <div class="row">
        <div>
          <modal :show.sync="modal0">
            <template slot="header">
              <h3 class="modal-title" id="exampleModalLabel" style="margin-top: 15px; color: #407ec1;">
                Financial Upload</h3>
            </template>
            <div>
              <vue-dropzone

                  ref="redDropZone"
                  id="dropzone2"
                  :options="dropzoneOptions"
                  @vdropzone-complete="uploadCompleted2"
                  @vdropzone-success="uploadSuccess2"
                  @vdropzone-error="uploadFailed2"
                  v-on:vdropzone-sending="sendingEvent"
              ></vue-dropzone>
            </div>
            <div class="row">
              <div class="col-md-12">
                <select v-model="selected" @change="onChange($event)" class="col-md-12 custom-select"
                        style="margin-top: 20px;">
                  <option v-for="bank in banksList" v-bind:key="bank">
                    {{ bank }}
                  </option>
                </select>
              </div>
            </div>
            <div class="row" style="margin-top: 20px;">
              <div class="col-md-12">
                <base-input placeholder="rename file" v-model="newFileName2"></base-input>
              </div>
            </div>
            <template slot="footer">
              <base-button type="secondary" @click="clearUploads2">Clear</base-button>
              <base-button type="primary" style="background-color: #407ec1;" @click="startProcessingQueue">Submit
              </base-button>
            </template>
          </modal>



          <modal :show.sync="modal1">
            <template slot="header">
              <h3 class="modal-title" id="exampleModalLabel" style="margin-top: 15px; color: #407ec1;"></h3>
            </template>
            <div class="col-md-12">
              <div style="margin-bottom: 20px;">
                {{ fileProps.filename }}
              </div>
              <base-input placeholder="rename file" id="filenameinput" v-model="newFileName"></base-input>
              <p></p>
            </div>
            <template slot="footer">
              <base-button type="primary" style="background-color: #407ec1;" @click="startProcessingQueue2">Submit
              </base-button>
            </template>
          </modal>

        </div>
      </div>
      <!-- End charts-->

      <!--Tables-->
      <!--<div class="row mt-5">
          <div class="col-xl-8 mb-5 mb-xl-0">
              <page-visits-table></page-visits-table>
          </div>
          <div class="col-xl-4">
              <social-traffic-table></social-traffic-table>
          </div>
      </div>-->
      <!--End tables-->
    </div>

  </div>
</template>
<script>
// Charts
/*eslint-disable*/
import * as chartConfigs from '@/components/Charts/config';
import LineChart from '@/components/Charts/LineChart';
import BarChart from '@/components/Charts/BarChart';
import vue2Dropzone from 'vue2-dropzone'
import 'vue2-dropzone/dist/vue2Dropzone.min.css'

// Tables
import SocialTrafficTable from './Dashboard/SocialTrafficTable';
import PageVisitsTable from './Dashboard/PageVisitsTable';
import axios from 'axios';

let address = 'https://127.0.0.1:3002';
export default {
  components: {
    LineChart,
    BarChart,
    PageVisitsTable,
    SocialTrafficTable,
    vueDropzone: vue2Dropzone,
    axios
  },
  data() {
    return {
      banksList: [],
      selected: '',
      selected2: '',
      userID:'',
      modal0: false,
      fileProps: [],
      newFileName:'',
      newFileName2:'',
      modal1: false,
      bigLineChart: {
        allData: [
          [0, 20, 10, 30, 15, 40, 20, 60, 60],
          [0, 20, 5, 25, 10, 30, 15, 40, 40]
        ],
        activeIndex: 0,
        chartData: {
          datasets: [],
          labels: [],
        },
        extraOptions: chartConfigs.blueChartOptions,
      },
      redBarChart: {
        chartData: {
          labels: ['Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
          datasets: [{
            label: 'Sales',
            data: [25, 20, 30, 22, 17, 29]
          }]
        }
      },
      dropzoneOptions: {
        url: address + '/upload/new',
        thumbnailWidth: 150,
        maxFilesize: 100,
        headers: {
          "Accept": "*"
        },
        /*dictDefaultMessage: "Drop files here <br>or click to upload...",*/
        params: {'userID':'xyz','fileWrite':'aaa'},
        thumbnailHeight: 150,
        thumbnailMethod: 'crop',
        autoProcessQueue: false,
        addRemoveLinks: true,
        uploadMultiple: false
      },
      uploads: []
    };
  },
  methods: {
    filenamechecker2(){
      if (this.newFileName){
        return this.newFileName;
      }else {
        return this.newFileName2;
      }
    },
    processingFile(file){
      console.log('processing ' + file.name);
      this.modal1 = true;
      this.fileProps.filename = file.name;
    },
    /*renameFile(file) {
      console.log("renameFile", file);
      return "." + file.name.toLowerCase().split('.').pop()
    },*/
    smallfxn(){
      return this.newFileName + '.png';
    },
    onChange(event) {
      console.log(event.target.value);
      this.selected2 = event.target.value;
      this.$refs.redDropZone.setOption('paramName', this.selected2);
    },
    sendingEvent(file, xhr, formData) {
      formData.append('userID', 'user123');
    },
    initBigChart(index) {
      let chartData = {
        datasets: [
          {
            label: 'Performance',
            data: this.bigLineChart.allData[index]
          }
        ],
        labels: ['May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      };
      this.bigLineChart.chartData = chartData;
      this.bigLineChart.activeIndex = index;
    },
    uploadSuccess(file, response) {
      console.log(file, 'has been uploaded ', ' response ', response);
      console.log(file.name);
      console.log(file.upload.filename);
      let self = this;
      setTimeout(function () {
        for (let i = 0; i < self.uploads.length; i++) {

          if (self.uploads[i].filename == file.name) {
            console.log('found one');

            if (response === 'file saved') {
              self.uploads[i].uploadStatus = true;
              self.uploads[i].uploadMessage = 'Saved... Awaiting ingestion...';
              let fileextension = "." + file.name.toLowerCase().split('.').pop();
              console.log(self.userID+ "*" + self.newFileName + fileextension);
              self.checker(self.userID +"*"+ self.newFileName + fileextension);
            } else if (response === 'file exists') {
              self.uploads[i].uploadStatus = false;
              self.uploads[i].uploadMessage = 'File already exists.';
            }
          }
        }
      }, 1000);
      /*setTimeout(function (){
          this.uploads.find(upload => upload.filename === file.name).uploadStatus = 'Upload complete.';
      },1000);*/
    },
    uploadSuccess2(file, response) {
      console.log(file, 'has been uploaded ', ' response ', response);
      console.log(file.name);
      console.log(file.upload.filename);
      let self = this;
      setTimeout(function () {
        for (let i = 0; i < self.uploads.length; i++) {

          if (self.uploads[i].filename == file.name) {
            console.log('found one');

            if (response === 'file saved') {
              self.uploads[i].uploadStatus = true;
              self.uploads[i].uploadMessage = 'Saved... Awaiting ingestion...';
              let fileextension = "." + file.name.toLowerCase().split('.').pop();
              console.log(self.userID+ "*" + self.newFileName2 + fileextension);
              self.checker(self.userID+ "*" + self.newFileName2 + fileextension);
              console.log('checking ',file.name);
            } else if (response === 'file exists') {
              self.uploads[i].uploadStatus = false;
              self.uploads[i].uploadMessage = 'File already exists.';
            }
          }
        }
      }, 1000);
      /*setTimeout(function (){
          this.uploads.find(upload => upload.filename === file.name).uploadStatus = 'Upload complete.';
      },1000);*/
    },
    uploadFailed(file, message, error) {
      /*console.log(file, 'has failed uploading with error ', error , ' and message ' , message);*/
    },
    uploadFailed2(file, message, error) {
      /*console.log(file, 'has failed uploading with error ', error , ' and message ' , message);*/
    },
    uploadCompleted(response) {
      console.log(response, 'has completed the upload');
      let fileextension = "." + response.name.toLowerCase().split('.').pop();
      this.uploads.push({
        filename: response.name,
        tempFileName: this.filenamechecker() + fileextension,
        uploadStatus: true,
        uploadMessage: 'Uploading...',
        uploadTime: 500,
        number: this.uploads.length + 1
      });
    },
    filenamechecker(){
      if (this.newFileName){
        return this.newFileName;
      }else {
        return this.newFileName2;
      }
    },
    uploadCompleted2(response) {
      console.log(response, 'has completed the upload');
      let fileextension = "." + response.name.toLowerCase().split('.').pop();
      this.uploads.push({
        filename: response.name,
        tempFileName: this.filenamechecker() + fileextension,
        uploadStatus: true,
        uploadMessage: 'Uploading...',
        uploadTime: 500,
        number: this.uploads.length + 1
      });
      this.modal0 = false;
    },
    clearUploads() {
      this.$refs.blueDropZone.removeAllFiles();
      console.log('clearing files');
      this.uploads = [];
    },
    clearUploads2() {
      this.$refs.redDropZone.removeAllFiles();
      console.log('clearing files');
    },
    getBanks() {
      axios.post(address + '/banks/list', {
        firstName: 'Finn'
      })
          .then((response) => {
            console.log(response.data);
            for (let c = 0; c < response.data.length; c++) {
              this.banksList.push(response.data[c].bankName);
              console.log(response.data[c].bankName);
            }

          }, (error) => {
            console.log(error);
          });
    },
    checker(filename) {
      axios.post(address + '/upload/checker', {
        filename: filename
      })
          .then((response) => {
            console.log(response.data);
            let recover = this;
            if (response.data.status === false) {
              console.log(filename, ' not yet');
              setTimeout(function () {
                recover.checker(filename);
              }, 1000);
            } else if (response.data.status === true) {
              console.log('true');
              let filestring = filename.split("*");
              let filet = filestring[1];
              console.log(filet);
              for (let t = 0; t < recover.uploads.length; t++) {
                console.log(recover.uploads[t].filename);
                if (recover.uploads[t].tempFileName === filet) {
                  recover.uploads[t].uploadStatus = false;
                  recover.uploads[t].uploadMessage = 'Ingestion has been completed';
                }
              }
            }
          }, (error) => {
            console.log(error);
          });
    },
    startProcessingQueue() {
      this.$refs.redDropZone.setOption('headers', {"extension" : this.userID+'*'+this.newFileName2});
      this.$refs.redDropZone.processQueue();

      console.log('id ', this.userID+'*'+this.newFileName2);
    },
    startProcessingQueue2() {
      this.$refs.blueDropZone.setOption('headers', {"id" : this.userID+'*'+this.newFileName});
      this.modal1 = false;
      if (this.newFileName){
        this.$refs.blueDropZone.processQueue();
      }else if (!this.newFileName){
        this.$refs.blueDropZone.processQueue();
      }
    }
  },
  mounted() {
    this.initBigChart(0);
    this.getBanks();
    this.$refs.redDropZone.setOption('url', address + '/upload/financial');
    this.$refs.redDropZone.setOption('autoProcessQueue', false);
    this.$refs.redDropZone.setOption('acceptedFiles', 'application/pdf');
  },
  created() {
    let uri = window.location.href.split('?');
    if (uri.length == 2) {
      let vars = uri[1].split('&');
      let getVars = {};
      let tmp = '';
      vars.forEach(function (v) {
        tmp = v.split('=');
        if (tmp.length == 2)
          getVars[tmp[0]] = tmp[1];
      });
      console.log(getVars['userid']);
      this.userID = getVars['userid'];
      this.$refs.blueDropZone.setOption('headers', {"name" : getVars['userid']});
      this.$refs.redDropZone.setOption('headers', {"name" : getVars['userid']});
      // do
    }
  }
};
</script>
<style>
.vue-dropzone {
  border: 2px dashed #407ec1;
}

.dropzone {
  min-height: 350px;
}

.dropzone .dz-message {
  margin: 8em 0;
  color: #407ec1;
}
</style>
