import { Component, OnInit } from '@angular/core';
import { NgForm } from '@angular/forms';
import { NgbModal } from '@ng-bootstrap/ng-bootstrap';
import { MovieService } from '../../services/movie.service';

@Component({
  selector: 'app-movies-management',
  templateUrl: './movies-management.component.html',
  styleUrls: ['./movies-management.component.css']
})
export class MoviesManagementComponent implements OnInit {
  movies: any[] = [];
  selectedMovie: any = {};
  isEdit = false;

  constructor(
    private modalService: NgbModal,
    private movieService: MovieService
  ) {}

  ngOnInit(): void {
    this.loadMovies();
  }

  loadMovies(): void {
    this.movieService.getMovies().subscribe(movies => {
      this.movies = movies;
    });
  }

  openModal(content: any, movie?: any): void {
    if (movie) {
      this.isEdit = true;
      this.selectedMovie = { ...movie };
    } else {
      this.isEdit = false;
      this.selectedMovie = {};
    }
    this.modalService.open(content, { ariaLabelledBy: 'modal-basic-title' });
  }

  onSubmit(form: NgForm): void {
    if (form.valid) {
      if (this.isEdit) {
        this.movieService.editMovie(this.selectedMovie).subscribe(() => {
          this.loadMovies();
          this.modalService.dismissAll();
        });
      } else {
        this.movieService.addMovie(this.selectedMovie).subscribe(() => {
          this.loadMovies();
          this.modalService.dismissAll();
        });
      }
    }
  }

  editMovie(content: any, movie: any): void {
    this.openModal(content, movie);
  }

  deleteMovie(movie: any): void {
    if (confirm('Are you sure you want to delete this movie?')) {
      this.movieService.deleteMovie(movie.id).subscribe(() => {
        this.loadMovies();
      });
    }
  }
}
